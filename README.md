# KnockoutLearning
Knockout Demos For Self Reference

## Observables
You need to declare your model properties as observables, because these are special JavaScript objects that can notify subscribers about changes, and can automatically detect dependencies.
For example, rewrite the preceding view model object as follows:

```javascript
var myViewModel = {
    personName: ko.observable('Bob'), //personName is model property
    personAge: ko.observable(123)     //personAge is also a model property
};
```
### Reading and Writing Observables
**ko.observable** objects are actually *functions*.
* To **read** the observable’s current value, just call the observable with no parameters.
* To **write** a new value to the observable, call the observable and pass the new value as a parameter. 

You don’t have to change the view at all - the same **data-bind** syntax will keep working. The difference is that it’s now capable of detecting changes, and when it does, it will update the view automatically.

## Computed Observables
These are functions that are dependent on one or more other observables, and will automatically update whenever any of these dependencies change.

```javascript
self.makeModelName = ko.pureComputed(function () {
    return self.makeName + " " + self.modelName;
});

```
## Pure Computed Observables
If your computed observable simply calculates and returns a value based on some observable dependencies, then it’s better to declare it as a ko.pureComputed instead of a ko.computed. For example:

```javascript
self.makeModelName = ko.pureComputed(function () {
    return self.makeName + " " + self.modelName;
});
```
This feature **Prevents memory leaks** and **Reduces Computation Overhead**

## Observable Arrays
If you want to detect and respond to changes on one object, you’d use **observables**. If you want to detect and respond to changes of a collection of things, use an **observableArray**.

```javascript
var myObservableArray = ko.observableArray();    // Initially an empty array
myObservableArray.push('Some value');            // Adds the value and notifies observers
```
## Debugging assist
These two helper functions can help a lot during debugging your knockout code. Use them on browser console. These helper functions allow you to identify the data associated with a DOM element:

* ko.dataFor(element) - returns the data that was available for binding against the element
* ko.contextFor(element) - returns the entire **binng context** that was available to the DOM element.

## Managing ‘this’
There is a popular convention for managing **this**. If your viewmodel’s constructor copies a reference to this into a different variable (traditionally called self), you can then use self throughout your viewmodel and don’t have to worry about it being redefined to refer to something else. For example:

```javascript
function AppViewModel() {
    var self = this;
    self.name = ko.observable('Swapnil');
}
```
