# Angular

## 1 - Setup with Angular CLI
<details>
<summary>Installation</summary>

- install node + npm
- install angular CLI

</details>

<details>
<summary>Global styles</summary>

- global style files could be added to `angular.json`

</details>

<details>
<summary>Common commands</summary>

```bash
# create a project
ng new <project-name>

# run the app in dev mode
ng serve

# build for production
ng build --prod

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

## 4 - Dynamic Components

<details>
<summary>General info</summary>

- components, which are loaded programmatically
  - declarative with `*ngIf` (better if we can use this approach)
  - programmatic with Dynamic Component Loader (mostly when we want to create some external library)
    - component created and added to DOM via code (imperatively)
    - component is added and managed by a developer

</details>

<details>
<summary>Preparing Programmatic Creation</summary>

- import to auth component `AlertComponent`
```TypeScript
private showErrorAlert(message: string) {}
```
- is valid TS code, but not valid for angular, won't work
  - Angular doest lots of things to instantiate a component (change detection in the DOM)
  - need component factory
```TypeScript
// won't work
const alertComponent = new AlertComponent();

// with component factory
constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

private showErrorAlert(...) {
  // pass the component type here
  // returns not component but component factory
  const alertComponentFactory = this.componentFactoryResolver.resolveComponentFactory(AlertComponent);
}
```
- now need a place to attach that component
- can't attach with `@ViewChild()`, need viewContainerRef (object managed by angular, which gives angular a reference to a place in the DOM with which it can interact)
```TypeScript
// placeholder.directive.ts
@Directive({
  selector: '[appPlaceholder]'
})
export class PlaceholderDirective {
  // pointer to where this directive is going to be used
  // has useful methods to create a component in that place
  constructor(public viewContainerRef: ViewContainerRef) {}
}
```
- access the directive
```HTML
<ng-template appPlaceholder></ng-template>
```
```TypeScript
// type, will look for the 1st occurrence in the component
@ViewChild(PlaceholderDirective) alertHost: PlaceholderDirective;

private showErrorAlert(...) {
  // ...
  const hostViewContainerRef = this.alertHost.viewContainerRef;
  // to clean all that was here before
  hostViewContainerRef.clear();
  hostViewContainerRef.createComponent(alertComponentFactory);
}
```

</details>

<details>
<summary>Entry Components</summary>

- error before Angular 9 (ivi has no such error) when creating the component manually
- angular checks for the component either in module declarations or in router
- but it doesn't work when we create the component manually
- have to prepare angular that it will be created at some point
```TypeScript
@NgModule({
  // ...
  // only for components, which are not created via selector <app-component>
  // or in router
  entryComponents: [
    AlertComponent
  ]
})
```

</details>

<details>
<summary>Data binding and Event binding</summary>

```TypeScript
private showErrorAlert(...) {
  // ...
  const componentRef = hostViewContainerRef.createComponent(alertComponentFactory);
  // instance has our props
  componentRef.instance.message = message;
  this.closeSub = componentRef.instance.close.subscribe(() => {
    this.closeSub.unsubscribe();
    hostViewContainerRef.clear();
  });
}

// when the upper component is destroyed
ngOnDestroy() {
  this.closeSub.unsubscribe();
}
```

</details>

<details>
<summary>Learn more</summary>

- [Dynamic component loader](https://angular.io/guide/dynamic-component-loader)

</details>

## 5 - Directives
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

## 6 - Models
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

## 7 - Services
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
<summary>Usage strategies</summary>

- AppModule => app-wide (same instance) === {providedIn: 'root'} => root injector => use by default
- Component => component-tree (new instance) => component specific injector => use if needed
- Eager-loaded modules => app-wide, but if included into both AppModule and LazyModule === new instance! => root injector / child injector => never use, unexpected issues
- Lazy-loaded module => module-lazy-wide (new instance) => child injector => use only when needed

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

## 8 - Routing
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

## 9 - Pipes
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

## 10 - Forms (Template Driven)
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

## 11 - Forms (Reactive)
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

## 12 - Modules
<details>
<summary>General info</summary>

- bundles different pieces into one package (components, directives, services, pipes, etc)
- have to group because Angular doesn't scan the files, have to inform what will be used
- requires at least 1 module (AppModule) but may be split into multiple modules
- Angular analyzes NgModules to understand your app and its features
- define all the building blocks your app uses: Components, Directives, Services, etc.
- core Angular features are wrapped in Angular modules (ex. FormsModule) to load them only when needed
- custom modules mostly for big projects
- gives Angular info on which features to use
- can't use a feature / building block without including it in a module

</details>

<details>
<summary>Analyzing the AppModule</summary>

- the service could be used not only in the module it's provided in
- bootstrap typically includes only one root component but if there are more components, will create a different root, will be detached from other components 
- every module in Angular works on its own, they don't communicate with each other, we can use the declared components only in the module
- have to export to be available where the module is imported
```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';

@NgModule({
  // components, directives, pipes
  declarations: [],
  // modules
  imports: [],
  // for exported features to use in other modules
  exports: [],
  // root needed on start component
  bootstrap: [],
  // services, interceptors
  providers: [],
  // for the case when we want to create a dynamic component in code
  entryComponents: []
})
export class AppModule {}
```

</details>

<details>
<summary>Feature modules</summary>

- groups together the pieces, which are used in the certain area of the app (recipes, shopping-list, auth)
- leaner code, easy to work, needed for future optimization (lazy loading)
```TypeScript
// recipes.module.ts
@NgModule({
  // remove from AppModule
  declarations: [RecipesComponent, ...],
  exports: [RecipesComponent, ...]
})
export class RecipesModule {}
```
- `imports: [RecipesModule]` to the app module
- error: router-outlet is not a known element => using but this directive is provided by Angular, available from RouterModule
- RouterModule is used not only to config the routes, but also provides all the directives to use (like router-outlet)
- it's available in AppModule, but not in the RecipesModule (the modules live on their own, have to import!)
- only services could be set up once in the app module and used in different modules
1. `imports: [RouterModule]` for using router
2. `imports: [CommonModule]` not `BrowserModule` - special case (only one) as `BrowserModule` is used only once in the AppModule, does more than `ngIf` and `ngFor`, also some app startup work that only needs to run once
3. `imports: [ReactiveFormsModule]` to use forms

</details>

<details>
<summary>Adding routes to Feature modules</summary>

- `imports: [RouterModule.forChild(routes)]` will automatically merge these routes with root routes (.forRoot)
```TypeScript
// recipes-routing.module.ts
const routes: Routes = [{
  path: 'recipes', ... // + all the child routes, remove from app-routing
}];
@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class RecipesRoutingModule {}
```
- import to RecipesModule
- now routes are part of the general routing config (since we import the RecipesModule to AppModule)
- need not only add Components to router but have to declare them on the module level or there will be an error
- but now we load the components via router, no need to export them in the RecipesModule, Angular knows how to load components because of router

</details>

<details>
<summary>Shared modules</summary>

- to avoid code duplication we can outsource the shared features into the shared module and import where needed
- can have multiple shared modules
```TypeScript
// shared.module.ts
@NgModule({
  declarations: [AlertComponent, PlaceholderDirective, ...],
  imports: [CommonModule],
  exports: [AlertComponent, PlaceholderDirective, CommonModule, ...],
  entryComponents: [AlertComponent]
})
export class SharedModule {}
```
- here we just centralize the functionality, so need to export all the features to use in other modules
- can only declare directives once!
- can import modules several times in different modules
- imports are ok, but declarations are not => get an error
- the solution: to export from module and to import module to use it in the other module

</details>

<details>
<summary>Core modules</summary>

- to make the app module leaner
- can use the core module to move the services from AppModule => CoreModule (but `{providedIn: 'root'}` is better)
- for interceptors still good to use CoreModule
```TypeScript
// core.module.ts
@NgModule({
  providers: [
    // if not in 'root'
    RecipesService,
    ...,
    {
      provide: HTTP_INTERCEPTOR,
      ...
    }
  ]
})
export class CoreModule {}
```
- don't need to export services (automatically injected on the root level)
- but still need to import the CoreModule in the AppModule

</details>

<details>
<summary>Learn more</summary>

- [NgModules](https://angular.io/guide/ngmodules)
- [NgModule FAQ](https://angular.io/guide/ngmodule-faq)

</details>

## 13 - Observables
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

## 14 - Http
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

## 15 - Interceptors
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

## 16 - Authentication
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

<details>
<summary>Adding the token to outgoing requests</summary>

- In the data-storage.service.ts
```TypeScript
// DataStorageService
constructor(private authService: AuthService) {}
```
- Update auth service to be able to fetch data about user on demand
  - can store token in a variable, but there is a better way
  - use `BehaviorSubject` almost = `Subject` but gives the subscribers immediate access to the previously emitted value even if they haven't subscribed at the point of time when the value was emitted. That means we can get access to the currently active user even if we only subscribe after that user has been emitted, so when we fetch data and we only need the token at this point even if the user logged in before that time, we get the access to this latest user, therefore `BehaviorSubject` needs to be initialized with the starting value.
- Add to the data storage service where we fetch recipes. Operator `take()` gives the value `(1)` time and automatically unsubscribes. Because we need the user only when we fetch recipes, but not constantly.
```TypeScript
this.authService.user.pipe(take(1)).subscribe();
```
- Pipe user observable and http observable into one bigger observable. `exhaustMap()` waits for the 1st observable (user) to complete after we `take(1)` user, `exhaustMap(user => this.http...)` observable will replace out user observable in the higher observable chain
```TypeScript
....user.pipe(take(1), exhaustMap(user => this.http...), map(recipes => {}));
```
- Add the token either as a query string (param) or in the second argument of the `http` method
```TypeScript
'....json?auth=' + user.token
{
  // from @angular/common/http
  params: new HttpParams().set('auth', user.token)
}
```
- if the token is not valid => error but we add logout when token is expired

</details>

<details>
<summary>Attaching the token with an interceptor</summary>

- don't add `{providedIn: 'root'}`, interceptors provided differently
```TypeScript
// auth-interceptor.service.ts
// AuthInterceptorService
// @angular/common/http
implements HttpInterceptor
intercept(req: HttpRequest<any>, next: HttpHandler) {
  return next.handle(req);
}
```
- inject `AuthService` to get user and `this.authService.user.subscribe();`
- use `exhaustMap()` to return a request observable
```TypeScript
const modReq = req.clone({params: ...});
exhaustMap(user => next.handle(modReq));
```
- now interceptor will add token to all outgoing requests
- provide in module `HTTP_INTERCEPTORS`
- can specify either url or `if (!user) { return next.handle(req); }`
- fails on login because we have no user yet (= null in `BehaviorSubject`)

</details>

<details>
<summary>Adding logout</summary>

```TypeScript
// auth.service.ts
logout() {
  this.user.next(null);
  this.router.navigate(['/auth']);
}
```
- add `onLogout()`to where needed (ex. click on logout button in header)
- redirect in service because we have only 1 place to login but multiple to logout

</details>

<details>
<summary>Adding auto-login</summary>

- to keep the logged in state on reload
- store user either in `localStorage` or use cookie
- in `handleAuth` inside `AuthService` add save to local storage
```TypeScript
localStorage.setItem('userData', JSON.stringify(user));
```
- add autoLogin method
```TypeScript
autoLogin() {
  const userData = JSON.parse(localStorage.getItem('userData'));

  if (!userData) {
    return;
  }

  const loadedUser = new User(userData.email, ...);

  if (loadedUser.token) {
    this.user.next(loadedUser);
  }
}
```
- convert date string into Date (in JSON it's a string)
- use the method inside app component (first entry basically)

</details>

<details>
<summary>Adding auto logout</summary>

- need to clear user on token expired
- in auth service in logout clear the `localStorage.removeItem('userData');`
- set a timer for auto logout
```TypeScript
autoLogout(expirationDuration: number) {
  this.logoutTimer = setTimeout(() => {
    this.logout();
  }, expirationDuration);
}
```
- clear the timer in logout (in case it still exists)
```TypeScript
logout() {
  // ...
  if (this.logoutTimer) {
    clearTimeout(this.logoutTimer);
  }
  this.logoutTimer = null;
}
```
- call autologout every time we emit new user

</details>

<details>
<summary>Adding AuthGuard</summary>

- to prevent visiting for unauthorized users
- add `auth.guard.ts`
```TypeScript
// AuthGuard
implements CanActivate {
  canActivate(route: ActivatedRouteSnapshot, router: RouterStateSnapshot):
    boolean |
    Promise<boolean> |
    Observable<boolean> {
    return this.authService.user.pipe(map(user => !!user));
  }
}
```
- but we want to navigate
  - earlier with `tap` operator
  - now with `urlTree`
```TypeScript
<boolean | urlTree>
map(user => {
  const isAuth = !!user;

  if (isAuth) {
    return true;
  }

  return this.router.createUrlTree(['/auth']);
});
```
- don't set constant subscription, add `take(1)` before map

</details>

<details>
<summary>Useful links</summary>

- [Firebase Auth REST API](https://firebase.google.com/docs/reference/rest/auth)
- [JSON Web Tokens](https://jwt.io/)

</details>

## 17 - Lazy loading
<details>
<summary>General info</summary>

- separating the code into modules makes it easier to work with, but doesn't improve the performance
- by default (without lazy loading) all the modules are loaded from the start (for all routes: `/`, `/admin`, `/user`, `/recipes`, ...) even when we don't navigate there
- so we want to load like that:
```
'path' => FeatureModule
'/' => AppModule / CoreModule
'/admin' => AdminModule
'/user' => UserModule
'/recipes' => RecipesModule
...
```

</details>

<details>
<summary>Implementing lazy loading</summary>

- check files sizes in the network panel of the dev tools
- have to register the routes for the module (feature module needs to bring its own routes for lazy loading with `.forChild()`)
- have to change `path: ''` to the empty path
- add path to app-routing module for lazy loading to work
```TypeScript
// app-routing.module.ts
{
  path: 'recipes',
  // old syntax
  // recipes, not recipes-routing
  // angular doesn't know the class name, have to set
  loadChildren: './recipes/recipes.module#RecipesModule'
  // new syntax (old could not work in the new versions)
  loadChildren: () => import('./recipes/recipes.module').then(module => module.RecipesModule)
}
```
- `loadChildren` gives Angular the direction to only load the module when the user visits this path
- now the code is split and all the declarations will be put into separate code bundle, which will be downloaded on demand
- don't import in the top (even unused) files into the AppModule or will be loaded when the app starts
- also remove the module from `imports: []` => error (2 times imported)
- when we go to '/recipes', the RecipesModule will be loaded and we already will be on '/recipes', that's why change path to `''`

</details>

<details>
<summary>Preloading lazy loaded code</summary>

- to avoid delay can preload modules
```TypeScript
// app-routing.module.ts
.forRoot(routes, {preloadingStrategy: PreloadAllModules});
```
- default is `NoPreloading`
- `PreloadAllModules` - code is split, will be preloaded as soon as possible
- initial bundle is still small
- can build own preload strategies

</details>

## 18 - Ahead-of-Time Compilation

<details>
<summary>Ahead-of-Time vs Just-in-Time Compilation</summary>

1. Your code and templates include syntax only Angular understands (*ngFor etc)
2. TypeScript compiler compiles the code to JavaScript
3. Angular compiler (automatically included in the built code) compiles template syntax to JavaScript DOM instructions
4. JiT vs AoT
  - JiT - Angular template compiler runs in browser (at runtime)
    - the compiler is too large and affects the performance
    - nice to use for development
    - `ng serve` uses JiT compiler
  - AoT - Angular template compiler runs during build process (before the app is deployed)
    - here the compiler runs only before the app is deployed and not in the browser
    - AoT removes the compiler from the final bundle
    - good for production
    - `ng build --prod`

</details>

## 19 - Offline
## 20 - Testing

## 21 - Debugging
<details>
<summary>Notes</summary>

- find an error in the console
- using sourcemaps and breakpoints in browser
  - `sources` => `webpack` => `.` => `src`
- using `debugger;`
- using chrome extension Augury (access from dev tools)

</details>

## 22 - Deploy

<details>
<summary>Order</summary>

1. Use and check environment variables
2. Polish the code
3. `ng build --prod` uses ahead-of-time compilation
4. Deploy built artifacts (generated files) to static host (because it's only html css and js)
  - static host means it can run only html, css and js logic, not backend

</details>

<details>
<summary>Environment variables</summary>

- built-in feature in every Angular project
- `environments` directive may have several files
  - the name of the exported constant is the same
  - can add there API keys for different modes
  - for production Angular automatically swaps `environment.ts` => `environment.prod.ts`
  - to use just import where needed `import { environment } from '../environment/environment'` (don't add .prod here, Angular swaps those files automatically for different modes)

</details>

<details>
<summary>Deployment example (Firebase hosting)</summary>

1. build the project for production `ng build --prod`
2. need a static website host
  - AWS
  - Firebase hosting (don't need to have backend here also)
3. install firebase CLI -g (node.js and npm required)
4. `firebase login`
5. `firebase init` to connect the project to firebase project
6. add only `hosting` (other features if needed) here database is in case we use the firebase CDK for that but we already have firebase database setup (works without CLI already)
7. choose the project to connect
8. set public directory to `dist/ng-complete...`
9. configure as an SPA? y - to be sure that all the requests sent to the API will be redirected to the `index.html` (have to config the server so that it always hit the `index.html`, no matter what path is in the browser) but by default server is set to different path requests and if the url is unknown to the server => error, we have router but it's only client side and runs only if the server serves the request, so all the requests should be redirected to the `index.html` and since any request reaches this page, Angular router can load the content via router
10. do not overwrite `index.html`
11. run `firebase deploy`

</details>

<details>
<summary>Learn more</summary>

- [How to fix broken Routes after Deployment](https://academind.com/learn/angular/angular-q-a/#how-to-fix-broken-routes-after-deployment)

</details>

## 23 - Animation
## 24 - Universal