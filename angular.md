# Angular

- [To content](#readme.md)

## 1 - Setup with Angular CLI
<details>
<summary>Notes</summary>

- install node + npm
- install angular CLI
- global style files could be added to `angular.json`
```bash
# create a project
ng new <project-name>

# run the app
ng serve

# create a component
ng g c <component-name or path + name>

# create a directive
ng g d <directive-name>
```

</details>

## 2 - How the app is being built?
<details>
<summary>Notes</summary>

- don't import with `.ts` extensions, webpack adds it
```TypeScript
// main.ts
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```
```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
  // should be known components when Angular analyses index.html
  bootstrap: [AppComponent]
})
export class AppModule {}
```
```TypeScript
// app/app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: '...'
})
export class AppComponent {}
```
```HTML
<!-- index.html -->
<!doctype html>
<html>
<head></head>
<body>
  <app-root></app-root>
</html>
```

</details>

## 3 - Components
<details>
<summary>Component creation and data binding</summary>

```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';
// needed to use two-way binding
import { FormsModule } from '@angular/forms';
import { NameComponent } from './components/name/name.component';

@NgModule({
  declarations: [NameComponent],
  imports: [FormsModule]
})
export class AppModule {}
```
```TypeScript
// app/components/name/name.component.ts
import { Component } from '@angular/core';

@Component({
  // required, must be a unique string
  selector: 'app-name', // tag, mostly for components
  selector: '[appDir]', // attribute, mostly for directives
  selector: '.class', // can also use a class as a selector
  // required, only one of
  template: '<p>Some text</p>',
  templateUrl: './name.component.html',
  // optional, only one of
  styles: '',
  styleUrls: ['./name.component.css'] // scss / less also possible
})
export class NameComponent {
  title: string = 'Hello from name component!';
  name: string = 'Max';

  onButtonClick(evt: Event) {
    console.log(evt.target);
  }
}
```
```HTML
<!-- app/components/name/name.component.html -->
<app-name></app-name>
<p appDir></p>
<p class="class"></p>
<!-- data-binding - communication between business logic and view -->
<!-- no multiline expressions -->
<!-- resolved to a string -->
<!-- updated dynamically at runtime -->
<!-- string interpolation -->
<p>{{ title }}</p> <!-- Hello from name component! -->
<!-- property binding -->
<p [innerText]="title"></p>
<!-- DON'T! improper usage -->
<p [innerText]="{{ title }}"></p>

<!-- event-binding - reaction to events -->
<!-- $event - browser event of type Event -->
<button type="button" (click)="onButtonClick($event)">Click</button>

<!-- two-way binding -->
<!-- triggers input data and updates BL -->
<!-- when BL is updated programmatically, updates the input -->
<input type="text" [(ngModel)]="name">
<p>{{ name }}</p>
```

</details>

<details>
<summary>Binding to custom properties</summary>

- to pass value from parent to child component
```TypeScript
// app/components/child/child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent {
  // to allow access from the outside
  // (by default props are accessible
  // only from the inside of the component)
  // if object = same object (reference type)
  @Input() user: object;
  @Input('fieldLabel') label: string;
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<app-child [user]="{ name: 'Lala' }" fieldLabel="E-mail"></app-child>
```

</details>

<details>
<summary>Binding to custom events</summary>

- to inform parent from child
- `@Output() cardAdded = new EventEmitter<card>();` from `@ang/core` create a custom event in child
- `EventEmitter` is an object in Angular, which allows to emit custom events
- `onAddCardClick() { this.cardAdded.emit(card); }` emit the event from child
- `<app-child (cardAdded)="onCardAdded($event)">` bind from parent
- `@Output('cAdded') cardAdded = ...` use not `(cardAdded)="..."`, but `(cAdded)="..."`

</details>

<details>
<summary>Local References</summary>

- usage inside a template, for ex when we don't need two-way binding
- returns an HTML element
- `#locRef` to any element
- `(click)="onButtonClick(locRef)"` or `{{ locRef.value }}`

</details>

<details>
<summary>ViewChild</summary>

- to get access to the html element from ts file
- `@ViewChild(Component / 'localRef') element: ElementRef` from `@ang/core`
  - `Component` returns the first occurrence of the component in the app
  - `localRef` returns an element with this localRef
- `{ static: true / false }` true if we plan to use it inside `ngOnInit()` (for Angular < 9)
- `this.element.nativeElement` to use
- don't change the value via this approach

</details>

<details>
<summary>ContentChild and ng-content</summary>

- `<ng-content></ng-content>` hook to project html content from parent to child
- `<app-child>...</app-child>` without `ng-content` ... content is lost
- `#locRef` add to a parent's html
- `@ContentChild('locRef') element: ElementRef` from `@ang/core` to access `<ng-content>` from parent in child
- `this.element.nativeElement` to access html element
- `@ContentChild('locRef', { static: true })` < 9 ver `true` if we plan to access from `ngOnInit()`, `false` otherwise
- don't change the value via this approach

</details>

<details>
<summary>View Encapsulation</summary>

- `encapsulation: ViewEncapsulation.Emulated` from `@ang/core` add to the decorator
  - `Emulated` angular emulates shadow DOM (creates unique attributes)
  - `Native` uses shadow DOM (not supported by all browsers)
  - `None` no attributes added

</details>

<details>
<summary>Component lifecycle</summary>

0. `constructor()`
1. `ngOnChanges(changes: SimpleChanges)` from `@ang/core` multi, after bound props change, changes contains those props
2. `ngOnInit()` once, when the component is initiated
3. `ngDoCheck()` multi, during every change detection runs (by Angular)
4. `ngAfterContentInit()` once, after `<ng-content>` has been projected into the view, can't access `@ContentChild` before
5. `ngAfterContentChecked()` multi, change detection
6. `ngAfterViewInit()` once, after view and child views initiated
7. `ngAfterViewChecked()` multi, change detection
8. `ngOnDestroy()` once, when about to be destroyed (ex `*ngIf`), clean-up here

</details>

## 4 - Directives
<details>
<summary>Attribute built-in</summary>

- looks like a normal HTML attribute
- doesn't change DOM
- event and data bindings are possible
- multiple on one element
- `[ngStyle]="{ 'background-color': 'prop' }"` or `[ngStyle]="{ backgroundColor: 'prop' }"`
- `[ngClass]="{ 'class-name': boolean }"` or `[ngClass]="{ className: boolean }"`
- `ngSwitch` directive is also attribute, but cases are structural

</details>

<details>
<summary>Structural built-in</summary>

- looks like a normal HTML attribute with a leading `*`
- affects DOM (elements get added or removed)
- can't use multiple on one element (error!)
- if directive
  - `*ngIf="boolean; else noServer"` else is optional
  - `<ng-template #noServer>` to use else
- for directive
  - `*ngFor="let item of items; let i = index"` index is optional
- `*ngSwitchCase`

</details>

<details>
<summary>Attribute custom</summary>

```TypeScript
// highlight.directive.ts
import { Directive, ElementRef, Renderer2 } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private element: ElementRef, private renderer: Renderer2) {} // to access the element

  doSomething() {
    // to access directly, but in some cases could not yet get rendered
    this.element.nativeElement;

    // renderer is better (inject Renderer2)
    this.renderer.setStyle(this.element.nativeElement, 'color', 'green', ~flags); // like !important, etc
  }
}
```

</details>

<details>
<summary>Binding custom</summary>

```HTML
<!-- if not the same name for the prop -->
<p appDirName defaultColor="blue">
<!-- when the name of the prop is the same -->
<p [appDirName]="'blue'">
```

```TypeScript
import { Renderer2, HostListener, HostBinding, OnInit } from '@angular/core';

@Directive({
  selector: '[appDirName]'
})
export class SomeDirective implements OnInit {
  // to bind to a custom property
  @Input() defaultColor: string = 'transparent';
  // to bind to the same name as a directive selector
  @Input('appDirName') defaultColor: string = 'transparent';
  // have to set initial color not to get an error
  @HostBinding('style.backgroundColor') backgroundColor: string = transparent;
  // won't work on init
  @HostBinding('style.backgroundColor') backgroundColor: string = this.defaultColor;
  // works like adding an event listener on the tag, where the directive is used
  @HostListener('mouseenter') hover(eventData: Event) {
    this.renderer.setStyle(...);
    // now can be used instead of renderer
    this.backgroundColor = 'blue';
  }

  constructor(private renderer: Renderer2) {}

  // have to set color here to work on init
  ngOnInit() { this.backgroundColor = this.defaultColor; }
}
```

</details>

<details>
<summary>Structural custom</summary>

- `ng g d directive_name` to generate directive with Angular CLI
```HTML
<div *ngIf="condition">
  <p>Some content</p>
</div>

<!-- turns into -->
<ng-template [ngIf]="condition">
  <div>
    <p>Some content</p>
  </div>
</ng-template>
```

```TypeScript
// unless.directive.ts
import { Directive, Input, ViewContainerRef, TemplateRef } from '@angular/core';

@Directive({
  selector: '[appUnless]' // any name
})
export class UnlessDirective {
  @Input() set appUnless(condition: boolean) { // name === directory selector
    if (!condition) {
      this.vcRef.createEmbeddedView(this.templateRef);
    } else {
      this.vcRef.clear();
    }
  }

  constructor(
    private vcRef: ViewContainerRef, 
    private templateRef: TemplateRef<any>
  ) {}
}
```
- `<div *appUnless="condition">...</div>` to use

</details>

## 5 - Models
<details>
<summary>Usage</summary>

- `recipe.model.ts` and `RecipeModel` naming
- no decorator, just a simple class
- works like a blueprint
- props creation (2 ways)
  - `constructor(public name: string) {}` shortcut, provided by TypeScript
  - ```TypeScript
    public name: string;
    constructor(name: string) { this.name = name }
    ```

</details>

## 6 - Services
<details>
<summary>Usage, hierarchical injector</summary>

- `logging.service.ts` naming `LoggingService`
- common cases to use
  - for less connection between app parts
  - working with data
  - DRY
  - centralize functionality
- has no decorators
- NOT! `const loggingService = new LoggingService();` Angular has better way (hierarchical dependency injector)
  - injects dependency into our component automatically
  - `constructor(private logService: LoggingService) {}` to inform Angular that we require such an instance, type is required
  - `providers: [LoggingService]` to let Angular know, how to give us a dependency
- hierarchical dependency injector levels
  - module level - the highest: services, components
  - root component level - components
  - component level - current components and all the children
  - lower levels override higher (create a new instance of a service)

</details>

<details>
<summary>In other services</summary>

1. provide on module level
  - `providers: [LoggingService]` in app.module 
  - `@Injectable({ provideIn: 'root' })` inside the service, also for lazy load (Angular 6+)
2. import the service
3. `constructor(private loggingService: LoggingService) {}`
4. `@Injectable()` to allow injecting a service

</details>

<details>
<summary>Cross-component communication</summary>

- add a custom event to the service
- emit the event in one component
- subscribe to the event in another component (add the event via custom binding)

</details>

## 7 - Routing
<details>
<summary>Setting up</summary>

- needed for adding navigation URLs
- `imports: [AppRoutingModule]` add module to `app.module.ts`
- `<router-outlet></router-outlet>` directive to the html, where we want to load the components from routes
```TypeScript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
// import all the components
// declarations: [] is not needed, all the components are declared in the app.module.ts

// add routes before the class
const appRoutes: Routes = [{...}];

@NgModule({
  imports: [RouterModule.forRoot(appRoutes)], // register routes (add configuration)
  // or hack for old browsers and servers with full paths (not returning index.html on 404 error)
  imports: [RouterModule.forRoot(appRoutes, { useHash: true })],
  exports: [RouterModule] // export what should be imported and accessible in another module
})
export class AppRoutingModule {}
```
```TypeScript
// app.module.ts
@NgModule({
  imports: [AppRoutingModule]
})
```

</details>

<details>
<summary>Adding routes</summary>

```TypeScript
const appRoutes: Routes = [{
  path: '', // for starting (root) page
  path: 'users', // without `/` (error)
  path: ':id', // to use dynamic paths
  path: '**', // catches all paths, which are not specified, must be the last route
  component: ServerComponent, // which component should be displayed when the path will be reached
  redirectTo: 'path', // but without component
  pathMatch: 'full', // reconfigures the default 
  children: [{ route }], // array of routes, `<router-outlet>` required on parent component
  canActivate: [AuthGuard],
  canActivateChild: [AuthGuard],
  canDeactivate: [CanComponentDeactivate],
  canDeactivateChild: [CanComponentDeactivate],
  data: { message: 'Page not found!' }, // to pass some static data
  resolve: { server: ServerResolver } // to pass some dynamic data
}];
```

</details>

<details>
<summary>Links and navigation</summary>

Navigating via links
- `href="/recipes"` === type manually, works, but reloads the app
- `routerLink="/recipes"` or `[routerLink]="['/users', 'user']"` second (and more) path without `/`, angular catches the event and prevents default
- routes can be absolute and relative (from current component)
- `routerLinkActive="class-name"` could be added to a link or it's wrapper
- `[routerLinkActiveOptions]="{ exact: true }"` for exact path match (full)

Navigating programmatically
- `constructor(private router: Router) { }` from `@ang/router` inject
- `this.router.navigate(['/users', 'user'])` like in `[routerLink]`, but doesn't know about current route
- `route: ActivatedRoute` from `@ang/router` inject, contains current route object
- `this.router.navigate([...], { relativeTo: this.route })`
- `this.router.navigate([...], { relativeTo: this.route, queryParamsHandling: '...' })`
  - `merge` merges current + navigate to params
  - `preserve` to keep only current params

</details>

<details>
<summary>Dynamic paths parameters</summary>

- get parameters from paths like `:id`
- `constructor(private route: ActivatedRoute) {}` inject from `@ang/router`
- `this.route.snapshot.params['id']` to access the parameter in the initialization, not dynamic
- but by default Angular doesn't re-instantiate the component we currently in
- `this.route.params.subscribe((params: Params) => this.id = params['id])` for dynamical use the params observable
- don't need to unsubscribe, for this case Angular does it automatically on component is destroyed

</details>

<details>
<summary>Query parameters and fragments</summary>

Via links
- `[queryParams]="{ allowEdit: '1', id: '2' }"` to `?allowEdit=1&id=2` bindable property of router directive
- `[fragment]="'loading'"` to `#loading`

Programmatically
- `constructor(private router: Router)` from `@ang/router`
- `this.router.navigate(['/users', id, 'edit'], { queryParams: { allowEdit: '1' }, fragment: 'loading' })`
- `queryParamsHandling: 'preserve' / 'merge'` don't forget to add

Getting parameters and fragments
- `constructor(private route: ActivatedRoute)` from `@ang/router`
- `this.route.snapshot.queryParams / fragment` for static
- `this.route.queryParams / fragment.subscribe()` for dynamic

</details>

<details>
<summary>Guards: canActivate</summary>

- for guards it's enough to have a snapshot, because guards are always get executed (reloads)
- to protect the route, runs before entering the route
- `canActivate(Child): [AuthGuard]` add to the route to protect route + children or children only
- `auth-guard.service.ts` export `AuthGuard(Service)`
- `CanActivate(Child)` implements from `@ang/router`
- for ex add some fake service
  ```TypeScript
  export class AuthService {
    isLoggedIn = false;
    
    isAuthenticated() {
      return new Promise((resolve, reject) => {
        setTimeout(() => { resolve(this.isLoggedIn); }, 800);
      });
    }
    
    login() {
      // some logic
    }
  
    logout() {
      // some logic
    }
  }
  ```
- `AuthService` provide on the module level
- `@Injectable()` add to guard service, provide on the module level
- ```TypeScript
  constructor(private authService: AuthService, private router: Router) {}
  
  canActivate( // can run both async and static
    route: ActivatedRouteSnapshot, 
    state: RouterStateSnapshot // from @ang/router
  ): Observable<boolean> | Promise<boolean> | boolean { // from 'rxjs/Observable
    return this.authService.isAuthenticated()
      .then((authenticated: boolean) => {
        if (authenticated) { 
          return true; 
        } else {
          return false;
          // or
          this.router.navigate(['/']);
        }
      }
    }
  }
  ```

</details>

<details>
<summary>Guards: canDeactivate</summary>

- for example not to leave the page without saving the data in the form
- `canDeactivate(Child): [CanDeactivateGuard]` add to the route to protect route + children or children only
- `can-deactivate-guard.service.ts` export `CanDeactivateGuard(Service)`
- ```TypeScript
  export interface CanComponentDeactivate {
    canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
  }

  export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {
    canDeactivate(
      component: CanComponentDeactivate, 
      route: ActivatedRouteSnapshot, 
      state: RouterStateSnapshot, 
      nextState?: RouterStateSnapshot
    ): Observable<boolean> | Promise<boolean> | boolean {
      return component.canDeactivate();
    }
  }
  ```
- add logic to component
- ```TypeScript
  export class RecipeComponent implements CanComponentDeactivate {
    canDeactivate(): Observable<boolean> | Promise<boolean> | boolean {
      if (!this.allowEdit) {
        return true;
      }

      if (this.allowEdit && this.edited && !this.saved) {
        return 'Confirmation here resolved to boolean';
      } else {
        return true;
      }
    }
  }
  ```

</details>

<details>
<summary>Passing data to route</summary>

Plain data (static)
- `data: { message: 'Page not found!' }` add to the route
- access the data from component
- ```TypeScript
  constructor(private route: ActivatedRoute) { }

  doSomething() {
    this.route.snapshot.data['message']; // static
    this.route.data.subscribe((data: Data) => console.log(data['message'])); //dynamic
  }
  ```

Complex data (dynamic)
- need to use a resolver, which helps to run the code before the route is activated
- the resolver doesn't decide whether the component should or not be rendered, component always get rendered
- resolver does some preloading before the route activates (could also be done in `ngOnInit`, but that way the component initiated first and then the data fetches)
- `resolve: { server: ServerResolver }` add to the route
- `server-resolver.service.ts`
- provide the resolver on module level
- ```TypeScript
  export class ServerResolver(Service) implements Resolve<Server> { // from @angular/router
    resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Server> | Promise<Server> | Server {
      return this.serversService.getServer(+route.params['id']);
    }
  }
  ```
- `this.route.data.subscribe((data: Data) => this.server = data['server']);` access the data from the component

</details>

## 8 - Pipes
<details>
<summary>Usage</summary>

- to transform a value in the template (output) sync/async data
- used inside the template
- can be used on any output, even on `*ngFor` loop items

</details>

<details>
<summary>Built-in</summary>

```TypeScript
{{ data | uppercase }}
{{ new Date() | date:'fullDate' }} // with parameters (for multiple date:param1:param2)
{{ new Date() | date | uppercase }} // chaining, from left to right, order matters
```

</details>

<details>
<summary>Custom simple pipe</summary>

- add to module `declarations: [ShortenPipe]`
- `{{ name | shorten }}` usage in template
- `{{ name | shorten:10 }}` usage in template with params
```TypeScript
// shorten.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'shorten'
})
// not necessary, but good practice to implement interface
export class ShortenPipe implements PipeTransform {
  // without params
  transform(value: any) {
    if (value.length > 10) {
      return value.substr(0, 10) + '...';
    }

    return value;
  }

  // with params
  transform(value: any, limit: number) {
    if (value.length > limit) {
      return value.substr(0, limit) + '...';
    }

    return value;
  }
}
```

</details>

<details>
<summary>Custom complex pipe</summary>

```HTML
<input type="text" [(ngModel)]="filteredStatus">
<ul *ngFor="let server of servers | filter:filteredStatus:'status'">
  <li>...</li>
</ul>
```

```TypeScript
// filter.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  // there is an issue if we want to add a new item dynamically
  // the servers are added (without filter visible),
  // but inside filtered items don't update dynamically,
  // only when reapply filter (not a bug, ang doesn't reload the pipe on every change)
  // changing the input (filter string) will trigger update
  // but changing data (adding server) will not
  // otherwise angular will rerun pipe every time ANY! data on the page changes
  // bad performance
  // so set pure to false only when needed
  pure: false
})
export class FilterPipe implements PipeTransform {
  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0 || filterString === '') {
      return value;
    }

    const resultArray = [];

    for (const item of value) {
      if (item[propName] === filterString) {
        resultArray.push(item);
      }
    }

    return resultArray;
  }
}
```

</details>

<details>
<summary>Async pipes</summary>

- `appStatus = new Promise((resolve, reject) => setTimeout(() => resolve('stable'), 2000));`
- if we output `{{ appStatus }}` => `[object Object]` (ang doesn't watch the Promise, good for performance, we have to tell ang to watch)
- add async pipe `{{ appStatus | async}}` => `''` => 2000 after => `stable`
- `async` pipe recognizes Promise or Observable (automatically subscribes)

</details>

## 9 - Forms (Template Driven)
<details>
<summary>Basic idea</summary>

- view <= conception => logic
```HTML
<form>
  <input name="name" ...>
  <input name="email" ...>
</form>
```

```TypeScript
{
  value: {
    name: 'Max',
    email: 'test@test.com'
  },
  valid: true
}
```
- <b>template-driven</b> approach - angular infers the FormObject from the DOM
- <b>reactive</b> approach - form is created programmatically and synchronized with DOM

</details>

<details>
<summary>TD creation</summary>

- all the functionality is added to template
- `<form>` no `action="..."` or `method="..."` needed
- import `FormsModule` to the module
- angular automatically creates a form object for `<form>` in template, but doesn't detect the controls inside
- add `ngModel` to a control to register
- add html attr `name="..."`
- to submit add `(ngSubmit)="onSubmit()"` to a form
- to access the form use `<form (ngSubmit)="onSubmit(f)" #f>` local reference
- `onSubmit(form: HTMLFormElement) {}`
- to get the data object add `#f="ngForm"`
- `onSubmit(form: NgForm) {}` from `@ang/forms`
- could be also accessed via `@ViewChild('f') form: NgForm;`

</details>

<details>
<summary>TD Validation</summary>

- add to inputs angular directives
  - `required` works as directive and attribute
  - `email` directive
- angular adds both to form and control state classes like `ng-dirty`, `ng-touched`, `ng-valid`
- to enable native validation add `ngNativeValidate` to a control
- `[disabled]="!f.valid`
- `.ng-invalid.ng-touched` to not show error borders on the start (adds not valid class when first loads)
- `<input ... #email="ngModel">` like with ngForm on the form local reference and `<span *ngIf="!email.valid && email.touched">Error text</span>`

</details>

<details>
<summary>TD Preselected values</summary>

- `<input ... [ngModel]="valueString">` and `valueString = "some value";` in .ts file
- works because of prop binding, no need to use two-way binding
- if we need to show output on keydown, also can use a two-way binding `[{ngModel}]="property"`

</details>

<details>
<summary>TD Grouping controls</summary>

- can also validate a group
- to access from ts file add local reference to a group like in controls or form
```HTML
<div class="controls-wrapper" ngModelGroup="userData" #userData="ngModelGroup"></div>
```

</details>

<details>
<summary>TD Radio buttons</summary>

```TypeScript
public genders = ['male', 'female'];
```
```HTML
<div *ngFor="let gender of genders">
  <label>
    <!-- without preselected value -->
    <input type="radio" name="gender" ngModel [value]="gender">
    <!-- or with preselected value use property binding -->
    <input type="radio" name="gender" [ngModel]="..." [value]="gender">
    {{ gender }}
  </label>
</div>
```

</details>

<details>
<summary>TD Set and patch values</summary>

```TypeScript
@ViewChild('f') form: NgForm; // to access the form

// have to add all values, sets the whole form (via input name attribute)
this.form.setValue({
  userData: {
    username: suggestedName,
    email: ''
  },
  secret: 'pet',
  gender: 'male'
});

// accessible only on inner .form method in form container (NgForm)
// to patch only needed values (doesn't override other values)
this.form.form.patchValue({
  userData: {
    username: suggestedName
  }
});
```

</details>

<details>
<summary>TD Use form data</summary>

```TypeScript
this.form.value.userData.username; // group => input name attribute
this.form.value.questionAnswer; // input name attribute
```

</details>

<details>
<summary>TD Reset form</summary>

```TypeScript
// resets also specific classes (ng-pristine, ng-touched, ...)
// can pass value like in setValue to reset to some specific values
this.form.reset();
```

</details>

## 10 - Forms (Reactive)
<details>
<summary>R Creation</summary>

- `ReactiveFormsModule` from `@angular/forms` add on module level
- `form: FormGroup` from `@angular/forms`
- can initiate form when declare a variable, but better in the method, for example in `ngOnInit` or other, but before the template is initiated

```TypeScript
this.form = new FormGroup({
  // use the quotes because connected to HTML, otherwise may be optimized by webpack
  'username': new FormControl(null), // presetValue, syncValidator(s), asyncValidator(s)
  'gender': new FormControl('female')
})
```

</details>

<details>
<summary>R Sync form and HTML</summary>

- by default `<form>` is only created, but not connected to the ts form
- use directives from the ReactiveFormsModule to connect
- `<form [formGroup]="form">` prop binding needed because we pass here our created form
- don't add name attribute or validation on controls (not needed)
- `formControlName="username"` here we pass a string, prop binding is also available

</details>

<details>
<summary>R Submit a form</summary>

- same as in TD, but without `#f`, because already have the form in ts `(ngSubmit)="onSubmit()"`
- all the object, passed on form creation we can get as a value of a form

</details>

<details>
<summary>R Access to controls</summary>

- there can be an error/bug with accessing controls in the template (can't use casting) due to the way TS works and Angular parses templates (doesn't understand TS there)
```TypeScript
// contains the control of type FormControl
// .valid .touched ... also available
this.form.get('username'); // control
this.form.get('userData.username'); // group => control
```

</details>

<details>
<summary>R Grouping controls</summary>

- `FormGroup` can be used inside the actual form (which is also a `FormGroup`)
- on a view wrap controls and add `formGroupName="userData"`
```TypeScript
this.form = new FormGroup({
  'userData': new FormGroup({
    'username': new FromControl(null),
    'email': new FormControl(null)
  })
});
```

</details>

<details>
<summary>R Arrays of controls</summary>

```HTML
<button (click)="onAddHobby()">Add hobby</button>
<ul formArrayName="hobbies">
  <!-- add controls, access control name by index in the array -->
  <li *ngFor="le hobbyControl of form.get('hobbies').controls; let i = index">
    <input type="text" [formControlName]="i">
  </li>
</ul>
```
```TypeScript
this.form = new FormGroup({
  'hobbies': new FormArray([...]) // could be empty
});

onAddHobby() {
  const control = new FormControl(null);
  // here TS needs casting for the array part
  (<FormArray>this.form.get('hobbies')).push(control);
}
```

</details>

<details>
<summary>R Validation</summary>

- don't add attributes to html (like required), add in ts to a control
- `username: new FormControl(null, Validators.required)` from `@angular/corms` don't execute here, pass only the reference, Angular will execute the method when the control changes
- for multiple validators `[Validators.required, Validators.email]`
- to check validation don't forget to check only touched controls `!form.get('username').valid && form.get('username').touched`

</details>

<details>
<summary>R Custom validators</summary>

- validator is just a function, which runs when Angular checks the validity of the control and when control is changed
```TypeScript
forbiddenUsernames = ['Anna', 'Jack'];

// if we use this class inside the validator function, don't forget to bind
// when Angular calls the method, this doesn't refer to our class
[Validators.required, this.forbiddenNames.bind(this)]

// [s: string] ts syntax for the key to be interpreted as a string
// error is added to control (not form) object 'errors'
forbiddenNames(control: FormControl): {[s: string]: boolean} {
  if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
    return {
      'nameIsForbidden': true
    }
  }

  // if validation is successful, return null or nothing
  return null;
}
```

</details>

<details>
<summary>R Error codes</summary>

```TypeScript
// to check if our custom error exists
form.get('userData.username').errors['nameIsForbidden'];

// for built-in validators
form.get.('...').errors['required'];
```

</details>

<details>
<summary>R Custom async validators</summary>

- for example to check if the email or username are already exist in the database
- like with normal validators, single or array
- don't forget to bind class if using `this`
```TypeScript
'email': new FormControl(null, Validators.required, this.forbiddenEmails)

forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      if (control.value === 'test@test.com') {
        resolve({'isEmailForbidden': true});
      } else {
        resolve(null);
      }
    }, 1500);
  });

  return promise;
}

```

</details>

<details>
<summary>R Reacting to status and value changes</summary>

- available on both from and control
```TypeScript
this.form.valueChanges.subscribe((value) => console.log(value));
this.form.statusChanges.subscribe((status) => console.log(status)); // VALID PENDING
```

</details>

<details>
<summary>R Set and patch values and reset a form</summary>

```TypeScript
// to set values to the whole form use
this.form.setValue({...});

// to patch only some values use
this.form.patchValue({...});

// to reset the form use
this.form.reset(); // can also pass {} with values to reset to
```

</details>

## 11 - Modules
<details>
<summary>Notes</summary>

- bundles different pieces into one package
- custom modules mostly for big projects
- gives Angular info on which features to use
```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';

@NgModule({
  // components, directives, pipes
  declarations: [],
  // modules
  imports: [],
  // root needed on start component
  bootstrap: [],
  // services, interceptors
  providers: []
})
export class AppModule {}
```

</details>

## 12 - Observables
<details>
<summary>Theory</summary>

- <b>Observable</b> - something we observe like publisher (also known as subject), data source, most common:
  - user events
  - http requests
  - triggered in code
- <b>Observer</b> - our code, our subscription
- Handling data:
  - Data
  - Errors
  - Completion (not always complete)
- added from `'rxjs'` package, not a part of TypeScript or Angular
- no need to import if we use Angulars Observables
- need to import only when we use other Observables

</details>

<details>
<summary>Interval example</summary>

```TypeScript
import {OnInit, OnDestroy} from '@angular/core';
import {Interval, Subscription} from 'rxjs';

@Component({...})
export class NameComponent implements OnInit, OnDestroy {
  // some code here
  private intSubscription: Subscription;

  ngOnInit() {
    interval(1000).subscribe(count => console.log(count));

    // to be able to unsubscribe => prevents memory leaks
    this.intSubscription = interval(1000).subscribe(count => console.log(count));
  }

  ngOnDestroy() {
    this.intSubscription.unsubscribe();
  }
}
```

</details>

<details>
<summary>Custom</summary>

```TypeScript
// from 'rxjs', create - a function, rxjs passes
const customIntObservable = Observable.create(observer => { // rxjs passes the arg observer (listener) 
  let count = 0;
  
  setInterval(() => {
    observer.next(count); // next emits new value

    // when error, there is no complete, complete != error
    if (count > 3) {
      observer.error(new Error('Error message')); // error = observable is done, no need to unsubscribe
    }

    if (count === 5) {
      observer.complete(); // done, no args, just stops, unsubscribe not needed
    }

    count++;
  }, 1000);
});

this.ownIntSubscription = customIntObservable.subscribe(
  data => console.log(data), // 1 - data handler
  error => console.log(error), // 2 - error handler
  () => console.log('Complete!') // 3 - complete handler
);

ngOnDestroy() {
  this.ownIntSubscription.unsubscribe();
}
```

</details>

<details>
<summary>Operators</summary>

- to transform data before subscribing
- can transform in subscription, but operators are better and cleaner
- import operators from `'rxjs/operators'`
- there are a lot of different operators
- `tap` allows to execute code without altering the result
- ```TypeScript
  this.ownIntSubscription = this.customIntObservable.pipe(
    filter(data => data > 0),
    map((data: number) => 'Round: ' + (data + 1))
  ).subscribe();
  ```

</details>

<details>
<summary>Subject</summary>

- using instead of `EventEmitter` for cross-component communication through service: better, more efficient, operators available
- `activatedEmitter = new Subject<boolean>();` add to service from 'rxjs'
- `this.userService.activatedEmitter.next(true);` from the 1st component
- `this.userService.activatedEmitter.subscribe();` form the 2nd component
- don't forget to unsubscribe
- in Observable we call `.next()` only from the inside, but in Subject can be called from the outside
- perfect for cross-component communication (triggered by app when no server involved)
- `@Output()` still uses `EventEmitter`, Subject here is not suitable

</details>

## 13 - Http
<details>
<summary>Http and backend interaction</summary>

- Angular => [http request] server => [REST/GraphQL etc] database
- database => server => [http response] Angular
- HTTP verb (action) `POST, GET, PUT, PATCH ...`
- URL (API endpoint) `/post/1`
- Headers (metadata) `{'Content-type': 'application/json'}`
- Body (optional) `{title: 'New Post'}`

</details>

<details>
<summary>Sending a POST request</summary>

- `import { HttpClientModule } from '@angular/common/http';` to `imports: [..., HttpClientModule]` on module level
- inject http client on component level
- if using firebase, add `.json` to the URL (firebase requirement)
- `.post` method returns an observable, no need to unsubscribe (it'll complete in the end, also it's Angular feature)
- browsers first send `OPTIONS` request to check if `POST` is available
- if 200 => send actual `POST` request
```TypeScript
export class NameComponent {
  constructor(private http: HttpClientModule) {}

  // sending post to server
  onCreatePost(postData: {title: string}) {
    // if we don't subscribe to an observable, Angular won't send the request
    // because of optimization, not interested in response? why send?
    this.http.post('<url>', postData).subscribe(responseData => console.log(responseData));
  }
}
```

</details>

<details>
<summary>Getting data</summary>

- add a method to fetch posts, use it in `ngOnInit`, whenever you want to update posts
```TypeScript
private fetchPosts() {
  // same as with the POST, need to subscribe or won't be sent
  this.http.get('<url>').subscribe(posts => console.log(posts));
}
```

</details>

<details>
<summary>Transforming data using operators</summary>

- can transform inside subscribe method, but operators are better (cleaner code)
- outputting the data is simple, don't forget to add ui if there is no posts
```TypeScript
// post.model.ts
export interface Post {
  title: string;
  content: string;
  id?: string;
}

// adding types to our requests (all requests are generics, so we can add type to <...>)
// also possible in operator, but better on the request
.post<{name: string}>(...);

.get<{[key: string]: Post}>(...) // response body type
.pipe(map(responseData => {
  const posts = [];
  
  for (const key in responseData) {
    // good to check in 'for ... in' loop if we're not trying to access some prototype method
    if (responseData.hasOwnProperty(key)) {
      // use spread to copy an object to add some data
      // in firebase key is unique encrypted name, good for id and access later to update or delete posts
      posts.push({...responseData[key], id: key});
    }
  }

  return posts;
}))
.subscribe(posts => console.log(posts));
```
```TypeScript
public isFetching = false;

// can also add a loader
// don't forget to add !isFetching to no posts and posts display views
public fetchPosts() {
  this.isFetching = true;
  this.http.get(...).subscribe(() => this.isFetching = false);
}
```

</details>

<details>
<summary>Using a service for http requests</summary>

- it's better to use service for http handling and let the component be simple, only handling the template work
- move functions
```TypeScript
storePost(title: string, content: string) {
  // http.post() here
}

fetchPosts() {
  // http.get() here
}
```
- if the components are not interested in receiving data, can subscribe in service
- if data needed in the component, `return get/post` and don't subscribe
- or use `Subject` and `.next` method
- where using loader and fetching, don't forget to reset `isLoading` to `true` first!

</details>

<details>
<summary>Sending a delete request</summary>

- not always allowed by backend API
- add delete method to the service
```TypeScript
deletePosts() {
  return this.http.delete('url');
}
```
- get the data (subscribe to null the array) from component
```TypeScript
onClearPosts() {
  this.postsService.deletePosts().subscribe(() => this.posts = []);
}
```

</details>

<details>
<summary>Handling errors</summary>

- firebase settings to rules (simulate error to test)
- add a reaction to an error (different ways)
- pass 2nd argument to subscribe method, which handles error
```TypeScript
(error) => this.error = error.message;
```
- subject for using error handling (especially for cases when we do not subscribe in the components)
- add to service
```TypeScript
error = new Subject<string>(); // from rxjs
...
(error) => this.error.next(error.message);
```
- and subscribe in the component
```TypeScript
this.errorSub = this.postsService.error.subscribe((errorMsg) => {
  this.error = errorMsg; 
});

ngOnDestroy() {
  this.errorSub.unsubscribe();
}
```

</details>

<details>
<summary>Cases when error can occur in different situations</summary>

- there is also an operator to assist with errors, for example when we pipe data (not always http related)
- `throwError` from `rxjs/operators` is specific for this case also possible, wraps error into observable
```TypeScript
{ return throwError(errorResult); } // inside catchError
```
```TypeScript
// from 'rxjs/operators'
// need to pass something, which could be subscribed to (need to subscribe)
// subject if possible
.pipe(map(...), catchError(errorResponse => {
  // do something with the error (analytics or UI)
}));
```

</details>

<details>
<summary>Good practice for UI handling errors</summary>

- add a button to remove an error from the UI
- don't forget to reset isLoading and other props for correct messages on the view

</details>

<details>
<summary>Setting headers</summary>

- for auth (ex), some custom headers etc. (depends on server API)
- any http method has the last argument (post - 3rd) (get - 2nd), which is an object with some configurations
```TypeScript
// from '@angular/common/http
{ headers: new HttpHeaders ({
  'Custom header': 'Hello'
}) }
```

</details>

<details>
<summary>Setting query parameters</summary>

- also depends on what parameters are supported by server API
- add to the same object as for headers
```TypeScript
{
  params: new HttpParams().set('print', 'pretty')
}
```
- works the same as if you add `?print=pretty` to the URL, but params is more clear and better
- for more params
```TypeScript
let params = new HttpParams();
// append returns a new object
params = params.append('print', 'pretty');
params = params.append('custom', 'value');
{
  params: params
}
```

</details>

<details>
<summary>Observing different types of responses</summary>

- for the cases when we need not / not only body, but other props of response data (headers, status, etc)
- added to the same config object as query params or headers
```TypeScript
{
  observe: 'body' // default
  observe: 'response' // whole response
  observe: 'events' // a series of events encoded with numbers
  // like 4 = response
}
.pipe(tap(event => console.log(event)));
if (event.type === HttpEventType.response) {...}
```
- for ex needed to give info to the user if something is being sent etc

</details>

<details>
<summary>Changing the response body type</summary>

- also added to the same config object as headers etc
```TypeScript
{
  responseType: 'json' // default
  responseType: 'text'
  responseType: 'blob'
  ...
}
```

</details>

## 14 - Interceptors
<details>
<summary>General info</summary>

- when to use? for ex when we want to attach the same custom header to all our requests, more realistic when we need to auth user and send a header
- `auth-interceptor.service.ts` export `AuthInterceptorService`
- `implements HttpInterceptor` from `@angular/common/http`
```TypeScript
// next - function, which will forward the request
intercept(req: HttpRequest<any>, next) {...}
```
- interceptor runs a code before the request lives our app, we need to add next to allow the request continue its journey, otherwise error
```TypeScript
{
  console.log('Request is on its way');
  return next.handle(req);
}
```
- provide in app module in a special way
```TypeScript
providers: [{
  // from '@angular/common/http
  // a token how ang identifies that should be treated
  // as an http interceptor and run in the whole app
  provide: HTTP_INTERCEPTORS,
  useClass: AuthInterceptorService,
  // if > 1 interceptors
  multi: true
}]
```
- angular by default will run the interceptor with all the http methods, but we can configure the restriction inside the interceptor function
```TypeScript
intercept(...) {
  if (req.url === '...') {
    // do something
  }
}
```
- inside we can modify the request object (case with added headers), but req object itself is immutable
```TypeScript
const modifiedReq = req.clone({
  url: '...',
  headers: req.headers.append('Auth', 'some-value')
});
return next.handle(modifiedReq);
```

</details>

<details>
<summary>Response interceptors</summary>

- add something to `return next...` of the intercept function
```TypeScript
return next.handle(modifiedReq)
  // here in the interceptor we always get the events,
  // no matter what was chosen on the request http method
  .pipe(tap((event) => {
    if (event.type === HttpEventType.response) {
      console.log(event.body);
    }
  }));
```
- be careful not to change data to break the application

</details>

<details>
<summary>Multiple interceptors</summary>

- the order in the app module matters, the first will be executed first
```TypeScript
providers: [{
  provide: HTTP_INTERCEPTORS,
  useClass: AuthInterceptorService,
  multi: true
}, {
  provide: HTTP_INTERCEPTORS,
  useClass: LoggingInterceptorService,
  multi: true
}]
```

</details>

## 15 - Authentication
<details>
<summary>General info</summary>

<img width="500" src="./images/auth.jpg" alt="authentication process">

- user enters data on client
  - can't check on client
  - insecure
- send auth data to server to authenticate the user
- server validates user
  - if valid - sends a token to client (json web-token typically)
  - encoded (not encrypted) - string with lots of metadata
  - could be unpacked and read by a client
  - generated on the server with secret algorithm only server knows, so only the server can validate the incoming token for validity
- client stores token in browser localStorage
- when one more time client sends to a server a request, it attaches the stored token in header or query param
- can't generate, edit or change the token on the client (not secure!)

- traditionally (not SPA) we work with session (stored on server, state existed), in stateless server and client don't know about each other

</details>

<details>
<summary>Adding a sign up request</summary>

- `auth.service.ts` `AuthService`
- `@Injectable()` from `@angular/core`
- `constructor(private http: HttpClient) {}` inject http service from `@angular/http`
- add the interface of response data (good practice)
- add method to a class
```TypeScript
signup(email, password) {
  return this.http.post<AuthResponseData>('url', {
    email,
    password
  });
}
```

</details>

<details>
<summary>Sending the sign up request</summary>

- in the form containing the component
```TypeScript
onSubmit() {
  if (!form.valid) {
    return;
  }

  const {email, password} = form.value;

  this.authService.signup(email, password)
    .subscribe(data => console.log(data), error => {});

  form.reset();
}
```
- inject the service `constructor(private authService: AuthService) {}`
- don't forget to add `isLoggedIn` logic

</details>

<details>
<summary>Adding loading spinner</summary>

- add prop on top `isLoading = false;`
- on submit before sending the request set to true
- and back to false on success or errors

</details>

<details>
<summary>Adding an error handling</summary>

- add prop on top `error: string = null;`
- set an error message in error handler of the http request
- for custom error handling better to use in service with operator `catchError/throwError` (because have to wrap an observable to pass to the subscribe)
- in service add after the request
```TypeScript
.pipe(catchError(errorRes => {
  let errorMessage = 'Some default error message';

  if (!errorRes.error || !errorRes.error.error) {
    return throwError(errorMessage);
  }

  switch(errorRes.error.error) {
    case 'EMAIL_EXISTS':
      errorMessage = 'Email exists';
      break;
  }

  return throwError(errorMessage);
}))
```

</details>

<details>
<summary>Login handling</summary>

- also when 2 similar subscriptions handling
```TypeScript
onSubmit() {
  // ...
  let authObservable: Observable<AuthResponseData>;

  if (this.isLoginMode) {
    authObservable = this.authService.login(email, password);
  } else {
    authObservable = this.authService.signup(email, password);
  }

  authObservable.subscribe();
}
```

</details>

<details>
<summary>Handling errors in separate method</summary>

- remove code from `.pipe(catchError(...))` to other method
```TypeScript
// from @angular/http
private handleError(errorRes: HttpErrorResponse) {}
```
- use where we need to catch an error `catchError(this.handleError)`

</details>

<details>
<summary>Creating and storing user data</summary>

- create a user model (with user data and validation if token exists and not expired)
```TypeScript
export class User {
  constructor(
    public email: string,
    public id: string,
    private _token: string,
    private _tokenExpirationDate: Date
  ) {}
}

get token () {
  if (!this._tokenExpirationDate 
    || new Date() > this._tokenExpirationDate) {
      return null;
    }

    return this._token;
}
```
- add a user subject in the auth service `user = new Subject<User>();`
- emit a new user every time the user changes (login / logout / exp date / etc.)
- add tap operator after catchError for handling user data
```TypeScript
private handleAuthentication(email: string, id: string, token: string, expIn: number) {
  const expDate = new Date(new Date.getTime() + expIn * 1000);
  const user = new User(email, id, token, expDate);

  this.user.next(user);
}

tap(this.handleAuthentication());
```

</details>

<details>
<summary>Reflecting the Auth status in the UI</summary>

- add user navigation on success of login (not in the service is better if you don't want to mix UI and service)
```TypeScript
// AuthComponent
// from @angular/router
constructor(private router: Router) {}

resData => {
  // ...
  this.router.navigate(...);
}
```
- change controls in the header (and other dependable UI), add logout button (later based on token, for now on user)
```TypeScript
// HeaderComponent
constructor(private authService: AuthService) {}

ngOnInit() {
  this.userSub = this.authService.user.subscribe(
    user => this.isAuth = !!user
  );
}

ngOnDestroy() {
  this.useSub.unsubscribe();
}
```
- update the logic on the UI with `*ngIf`

</details>

## 16 - Offline
## 17 - Testing

## 18 - Debugging
<details>
<summary>Notes</summary>

- find an error in the console
- using sourcemaps and breakpoints in browser
  - `sources` => `webpack` => `.` => `src`
- using `debugger;`
- using chrome extension Augury (access from dev tools)

</details>

## 19 - Deploy

<details>
<summary>Order</summary>

1. Use and check environment variables
2. Polish the code
3. `ng build --prod` uses ahead-of-time compilation
4. Deploy built artifacts (generated files) to static host (because it's only html css and js)

</details>

## 20 - Animation
## 21 - Universal