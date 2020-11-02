# Web Components
<details>
<summary>What are web components?</summary>

- custom HTML element
  - register own HTML tags
- Shadow DOM
  - manage a separate DOM node tree for your own HTML elements (including CSS)
  - Shadow DOM is great for styles encapsulation
- Templates and Slots
  - gives the ability to pass the content into the custom element template
- HTML Imports (not continued because decided to switch to JS)
  - import HTML files

</details>

<details>
<summary>Why web components?</summary>

- encapsulate the logic and UI
- re-usable across one project
- also re-usable between apps and projects
- browser support is already ok but still not all browsers fully support this technology

</details>

<details>
<summary>How to create a custom element?</summary>

- should be an instance of `HTMLElement`
- basic creation without using shadow DOM (problems with global styles, element is added to the actual DOM)
```JavaScript
class Tooltip extends HTMLElement {
  constructor() {
    super();
    this._tooltipContainer = null;
    // working with custom attributes
    this._tooltipText = 'Default tooltip text';

    this._showTooltip = this._showTooltip.bind(this);
    this._hideTooltip = this._hideTooltip.bind(this);
  }

  connectedCallback() {
    if (this.hasAttribute('text')) {
      this._tooltipText = this.getAttribute('text');
    }

    const tooltipIcon = document.createElement('span');

    tooltipIcon.textContent = '?';
    // show content on hover
    tooltipIcon.addEventListener('mouseenter', this._showTooltip);
    tooltipIcon.addEventListener('mouseleave', this._hideTooltip);
    this.style.position = 'relative';
    this.appendChild(tooltipIcon);
  }

  _showTooltip() {
    this._tooltipContainer = document.createElement('div');
    this._tooltipContainer.textContent = this._tooltipText;
    this.style.position = 'absolute';
    this.appendChild(this._tooltipContainer);
  }

  _hideTooltip() {
    this.removeChild(this._tooltipContainer);
  }
}

// to define your own HTML tag
// has to consist of at least 2 words
// separated by '-' (not one word not to be confused with other HTML tags)
// when you add this tag to HTML,
// JS uses the class to create an instance
customElements.define('ev-tooltip', Tooltip);
```
```HTML
<ev-tooltip text="Some custom text here">
  Web Components
</ev-tooltip>
are great!
```
- using Shadow DOM (encapsulated component has it's own DOM)
- global styles do not affect the component
- use templates to add the content (like 'Web Components')
```JavaScript
class Tooltip extends HTMLElement {
  constructor() {
    // ... init
    // mode - can access from outside or not
    this.attachShadow({ mode: 'open' });
    // ... bindings
  }

  connectedCallback() {
    // ... attributes, listeners, styles
    // append the element to the shadow DOM
    this.shadowRoot.appendChild(tooltipIcon);
  }

  _showTooltip() {
    // ...
    // append the element to the shadow DOM
    this.shadowRoot.appendChild(this._tooltipContainer);
  }

  _hideTooltip() {
    // remove the element from the shadow DOM
    this.shadowRoot.removeChild(this._tooltipContainer);
  }
}
```

</details>

<details>
<summary>How to use HTML tag template to create the template?</summary>

```JavaScript
class Tooltip extends HTMLElement {
  constructor() {
    // ... init
    const template = document.querySelector('#tooltip-template');

    this.attachShadow({ mode: 'open' });
    this.shadowRoot.appendChild(template.content.cloneNode(true));
    // ... bindings
  }

  connectedCallback() {
    // ... check text attribute
    const tooltipIcon = this.shadowRoot.querySelector('span');
    // ... listeners, styles
  }

  _showTooltip() {}

  _hideTooltip() {}
}
```
```HTML
<template id="tooltip-template">
  <!-- add <slot> where the text to be added -->
  <slot>Default</slot><span>?</span>
</template>
```

</details>

<details>
<summary>How to create a template in JS file?</summary>

```JavaScript
class Tooltip extends HTMLElement {
  constructor() {
    // ... init
    this.attachShadow({ mode: 'open' });
    // instead of adding styles via JS, can define it here
    this.shadowRoot.innerHTML = `
      <style>
        span {
          position: relative;
        }

        div {
          position: absolute;
          z-index: 100;
        }
      </style>
      <slot>Default text</slot><span>?</span>
    `;
    // ... bindings
  }

  connectedCallback() {}

  _showTooltip() {}

  _hideTooltip() {}
}
```

</details>

<details>
<summary>How to create an extended built-in element?</summary>

```JavaScript
class ConfirmLink extends HTMLAnchorElement {
  connectedCallback() {
    this.addEventListener('click', evt => {
      if (!confirm('Do you really want to leave?')) {
        evt.preventDefault();
      }
    });
  }
}

// for extended elements have to pass the tag to be extended
customElements.define('ev-confirm-link', ConfirmLink, { extends: 'a' });
```
```HTML
<a is="ev-confirm-link" href="https://google.com">Google</a>
```

</details>

<details>
<summary>What is a web component lifecycle?</summary>

1. element created `constructor()` basic initializations
2. element attached to the DOM `connectedCallback()` DOM initializations
3. observed attribute updated `attributeChangedCallback()` update data and DOM
4. element detached from the DOM `disconnectedCallback()` cleanup work

</details>

<details>
<summary>How to add several slots?</summary>

```JavaScript
class Modal extends HTMLElement {
  constructor() {
    this.attachShadow({ mode: 'open' });
    // unnamed slots will contain all the rest content inside
    this.shadowRoot.innerHTML = `
      <div class="modal">
        <header>
          <slot name="title">Default title</slot>
        </header>
        <slot>Default message</slot>
      </div>
    `;
  }
}

customElement.define('ev-modal', Modal);
```
```HTML
<ev-modal>
  <h1 slot="title">Some title</h1>
  <p>Main content</p>
</ev-modal>
```

</details>

<details>
<summary>How to react to changes inside the slot from the component?</summary>

```JavaScript
class Modal extends HTMLElement {
  constructor() {
    this.attachShadow({ mode: 'open' });
    this.shadowRoot.innerHTML = `
      <div class="modal">
        <header>
          <slot name="title">Default title</slot>
        </header>
        <slot>Default message</slot>
      </div>
    `;

    const slots = this.shadowRoot.querySelectorAll('slot');

    slots[1].addEventListener('slotchange', evt => {
      console.log(slots[1].assignedNodes());
    });
  }
}
```

</details>

<details>
<summary>How to work with and style slots?</summary>

- content added inside the `<slot>` tag is not rendered as a part of the shadow DOM, just normal DOM
- can be styled normally (as all the elements in the light DOM), shadow DOM styles are not applied
- can style slotted content with `::slotted(*)` selector from the shadow DOM, but only the direct children
- normal styles will override the shadow DOM styles

</details>

<details>
<summary>How to style the host component?</summary>

- from the outside just use the custom element selector (ex: `ev-tooltip`)
- from the inside use `:host` selector
- from the inside on condition `:host(.class-name)`
- from the inside with the context (ex: wrapped in `<p><span></span></p>` = `:host-context(p span)`)
- variables set outside and applied inside do work
```CSS
/* light DOM */
:root {
  --bg-primary: #eeeeee;
}

/* component */
:host {
  background-color: var(--bg-primary);
  /* or with fallback color */
  background-color: var(--bg-primary, #ffff00);
}
```

</details>

<details>
<summary>How to update custom attributes?</summary>

```JavaScript
class Tooltip extends HTMLElement {
  constructor() {}

  connectedCallback() {}

  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue === newValue) {
      return;
    }

    if (name === 'text') {
      this._tooltipText = newValue;
    }
  }

  // to set the attribute for observation
  static get observedAttributes() {
    // array of attributes to track
    return ['text', 'class'];
  }

  _showTooltip() {}

  _hideTooltip() {}
}
```

</details>

<details>
<summary>How to add the custom listeners?</summary>

```JavaScript
class Modal extends HTMLElement {
  constructor() {
    this.attachShadow({ mode: 'open' });
    this.shadowRoot.innerHTML = `
      <div class="modal">
        <header>
          <slot name="title">Default title</slot>
        </header>
        <slot>Default message</slot>
        <p class="buttons">
          <button type="button" class="cancel">Cancel</button>
          <button type="button" class="confirm">Ok</button>
        </p>
      </div>
    `;

    const cancelButton = this.shadowRoot.querySelector('.cancel');
    const confirmButton = this.shadowRoot.querySelector('.confirm');

    cancelButton.addEventListener('click', (evt) => {
      this._hide();
      
      // will be available on the button only
      const cancelEvent = new Event('cancel');
      const cancelEvent = new Event('cancel', { bubbles: true });
      // set composed to true to allow leaving the shadow DOM
      const cancelEvent = new Event('cancel', { 
        bubbles: true,
        composed: true 
      });

      evt.target.dispatchEvent(cancelEvent);
    });
  }

  _hide() {}

  _cancel() {
    // or dispatch event here
    this.hide();

    const cancelEvent = new Event('cancel');

    this.dispatchEvent(cancelEvent);
  }
}
```
```JavaScript
// main.js
const modal = document.querySelector('ev-modal');

modal.addEventListener('confirm', () => {});
modal.addEventListener('cancel', () => {});
```

</details>

<details>
<summary>How to do the cleanup work when the component is removed?</summary>

```JavaScript
class Tooltip extends HTMLElement {
  constructor() {}

  connectedCallback() {}

  attributeChangedCallback() {}

  disconnectedCallback() {
    // cancel the http request
    // remove listeners
    // send log to statistics
    // etc cleanup work here
    this._tooltipIcon.removeListener('mouseenter', this._showTooltip);
    this._tooltipIcon.removeListener('mouseleave', this._hideTooltip);
  }

  static get observedAttributes() {}

  _showTooltip() {}

  _hideTooltip() {}
}
```

</details>

<details>
<summary>Learn more</summary>

- [Web Components on MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
- [Using templates and slots on MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_templates_and_slots)
- [Custom Elements v1: Reusable Web Components](https://developers.google.com/web/fundamentals/web-components/customelements)
- [Shadow DOM v1: Self-Contained Web Components](https://developers.google.com/web/fundamentals/web-components/shadowdom)

</details>