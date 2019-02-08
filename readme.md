# SelectInput ![](https://img.shields.io/github/tag/pecuchet/select-input.svg?label=version&style=flat) [![Maintainability](https://api.codeclimate.com/v1/badges/d97692a882ba7d6d2b78/maintainability)](https://codeclimate.com/github/pecuchet/select-input/maintainability)

Single-purpose select box/dropdown with an input field&mdash;without dependencies (ie11+).  
<br>
[> demo](https://pecuchet.github.io/select-input/)

## Installation
```
npm i -D @dotburo/select-input
```


## Usage
```
import SelectInput from 'select-input';

// Minimal parameters
let selectInput = new SelectInput('.select-input', {
    items: ['A', 'B', 'C', 'D']
});

// Listen to events, add a callback and show the list 
selectInput.on('selected', e => console.log(e.detail))
           .on('created', e => selectInput.getCurrent())
           .onDelete(item => window.confirm('Sure?'))
           .toggle(true);
```

## Available options (and their defaults)
```
{
    items: [],                              # Array of strings/numbers or of {value: String|Number} objects
    current: null,                          # Item to select on instantiation
    parent: null,                           # Parent element, to 
    maxHeight: 0,                           # Maximum height of the dropdown, `0` means no constraint
    proposal: 'Add {X} to the list?',       # Message to add an item to the list, {X} will be replaced
    sort: true,                             # Whether to sort the list
    order: 'desc',                          # Sort order
    removalIcon: '&times;'                  # HTML for deletion button in each item li-element
    placeHolder: 'Type to search',          # Input field place holder
    onDelete: null,                         # Callable, fired before deleting an item; return `false` to prevent deletion
    onCreate: null                          # Callable, fired before creatng an item; return `false` to prevent creation
}
```

## Events

- **selected**
- **created**
- **removed**

Event handlers can be bound with `instance.on()` or `instance.getElement().addEventListener()`. In browsers which
support `CustomEvent` the `detail` property of the event object contains the created, selected or removed item. 
For older browsers `instance.getCurrent()` will need to be used.

## Public methods

### instance.on(event, fn, el = null): instance
Listen to events, pass in and event name (`String`), a subscriber (`Function`) and optionally and event target (`Element`). 
If the latter is omitted, events are delegated to `instance.getElement()`.

### instance.onDelete(fn): instance
Pass a function to be called before deleting an item. If the function returns false, the item will not be removed.

### instance.onCreate(fn): instance
Pass a function to be called before creating an item. If the function returns false, the item will not be created.

### instance.toggle(show = false): instance
Show or hide the list

### instance.getElement(): HTMLElement
Return SelectInput's outermost element 

### instance.getItems(): array
Get all the items in the list as an array of objects

### instance.getCurrent(): object
Return the currently selected item of the list
 
### instance.findItem(value): object
Find an item in the list by its value (`String|Number`)

### instance.remove(): void
Unbind all events and clean up the DOM
