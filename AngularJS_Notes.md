# AngularJS Notes

> Exam-ready notes based on the provided **AngularJS** and **AngularJS Services** PDFs.  
> Focus: definitions, concepts, syntax, important directives, examples, and technical points.

---

# Part 1 — AngularJS

## 1. What is AngularJS?

**AngularJS** is a JavaScript framework used to build dynamic web applications and Rich Internet Applications (RIA).

### Main characteristics

- JavaScript-based framework.
- Supports client-side application development.
- Uses concepts such as MVC/MVVM, data binding, directives, controllers, services, filters and modules.
- Supports development of **Single Page Applications (SPA)**.
- Provides dependency injection.
- Supports reusable components.
- Supports unit testing and end-to-end testing.
- The provided notes describe AngularJS as cross-browser compatible and open source under the Apache 2.0 license.

---

## 2. Single Page Application (SPA)

A **Single Page Application** loads the main HTML page once and dynamically changes the content/view without reloading the entire page.

### Basic flow

```text
Browser
   ↓
index.html
   ↓
AngularJS Application
   ↓
Changes data/view dynamically
   ↓
UI is updated
```

This allows faster user interaction and avoids complete page reloads.

---

## 3. REST Web Services with AngularJS

AngularJS can communicate with RESTful web services using HTTP calls.

### Key points

- RESTful services are accessed through HTTP.
- Data is commonly exchanged in JSON format.
- AngularJS acts as the client.
- The web service acts as the server.

```text
AngularJS Application
        |
        | HTTP request
        v
   REST Web Service
        |
        | JSON response
        v
AngularJS Application
```

Example:

```javascript
$http.get("students.json").then(function(response) {
    $scope.students = response.data;
});
```

---

# 4. AngularJS Application Structure

An AngularJS application can be organized using:

- **Module**
- **Controller**
- **Scope**
- **View**
- **Services**
- **Directives**
- **Filters**

The provided AngularJS material describes an application as a module containing components and services. Modules can also be reused by other modules.

---

# 5. MVC Architecture

**MVC = Model + View + Controller**

MVC is a software design pattern that separates application responsibilities.

### Model

The **Model** manages application data, logic and rules.

Example:

```javascript
student = {
    name: "Amit",
    rollNo: 101
};
```

### View

The **View** is what the user sees.

Usually, it is the HTML/UI part of the application.

Example:

```html
<h1>{{student.name}}</h1>
```

### Controller

The **Controller** handles application logic and interaction between the Model and View.

Example:

```javascript
app.controller("studentCtrl", function($scope) {
    $scope.student = {
        name: "Amit",
        rollNo: 101
    };
});
```

### MVC flow

```text
User
  ↓
View
  ↓
Controller
  ↓
Model
  ↓
View updated
```

### Separation of concerns

MVC separates UI, application logic and data management so that each part has a clear responsibility.

---

# 6. MVVM in AngularJS

The provided material also explains AngularJS using the **MVVM (Model-View-ViewModel)** idea.

### Model

Contains application/domain data and related business/validation logic.

### View

Defines the structure, layout and appearance shown to the user.

### ViewModel

Acts as an intermediary between the View and Model.

In the provided AngularJS material:

- **Model** → Angular Service/Factory
- **View** → HTML template with data binding
- **ViewModel** → AngularJS Controller

### Benefits

- View and business logic can be developed more independently.
- UI can be redesigned without changing the Model/ViewModel.
- Model and ViewModel can be unit tested separately.

---

# 7. Two-Way Data Binding

**Two-way data binding** means synchronization between the Model and View.

If the model changes, the view reflects the change.

If the user changes a bound input value, the model also changes.

### Example

```html
<input type="text" ng-model="name">

<p>Hello {{name}}</p>
```

If the user enters:

```text
Akash
```

The paragraph automatically becomes:

```text
Hello Akash
```

### Important directive

`ng-model`

It connects an HTML input control with AngularJS application data.

---

# 8. Dependency Injection (DI)

**Dependency Injection** is a technique in which required dependencies are supplied to a component instead of the component creating them itself.

AngularJS uses dependency injection to provide services and other dependencies to controllers and components.

### Example

```javascript
app.controller("myCtrl", function($scope, $http) {

});
```

Here:

- `$scope` is injected.
- `$http` is injected.
- The controller can directly use them.

### Advantages

- Reduces tight coupling.
- Improves testability.
- Makes code easier to maintain.
- Makes reusable services possible.

---

# 9. AngularJS Features

Important AngularJS features from the provided material:

1. Data binding
2. Scope
3. Controllers
4. Services
5. Filters
6. Directives
7. Templates
8. Routing
9. Deep linking
10. Dependency Injection
11. Testing
12. Reusable components

---

# 10. Scope

A **scope** is a JavaScript object that acts as a connection between the controller and view.

The provided material describes Scope as the Model available to the current view.

It contains:

- Properties
- Methods

These can be accessed by both the controller and view.

### Example

```javascript
app.controller("myCtrl", function($scope) {
    $scope.carname = "Volvo";
});
```

HTML:

```html
<div ng-app="myApp" ng-controller="myCtrl">
    <h1>{{carname}}</h1>
</div>
```

Output:

```text
Volvo
```

### Remember

```text
Controller
    ↓
  $scope
    ↓
  View
```

---

# 11. Controllers

A **controller** is a JavaScript function/object responsible for controlling the flow of data in an AngularJS application.

A controller can contain:

- Properties
- Functions
- Application logic

It is connected to HTML using `ng-controller`.

### Example

```html
<div ng-app="myApp" ng-controller="studentCtrl">
    <p>{{student.fullName()}}</p>
</div>
```

```javascript
var app = angular.module("myApp", []);

app.controller("studentCtrl", function($scope) {

    $scope.student = {
        firstName: "Mahesh",
        lastName: "Parashar",

        fullName: function() {
            return this.firstName + " " + this.lastName;
        }
    };

});
```

---

# 12. AngularJS Modules

A **module** defines an AngularJS application or a part of an application.

### Creating a module

```javascript
var app = angular.module("myApp", []);
```

- `myApp` → module name
- `[]` → dependency list

### Using the module

```html
<body ng-app="myApp">
```

### Controller inside a module

```javascript
app.controller("myCtrl", function($scope) {
    $scope.name = "Amit";
});
```

### Module vs Application

```text
AngularJS Application
        |
      Module
   /    |     \
Controller Service Filter
```

Modules help organize and reuse application functionality.

---

# 13. Directives

**Directives** are special AngularJS attributes/elements that extend HTML with AngularJS behavior.

Most built-in directives use the `ng-` prefix.

### Important directives

| Directive | Purpose |
|---|---|
| `ng-app` | Initializes/bootstraps AngularJS application |
| `ng-init` | Initializes application data |
| `ng-model` | Creates/binds model data |
| `ng-bind` | Binds application data to HTML |
| `ng-controller` | Associates a controller with a view |
| `ng-repeat` | Repeats HTML for collection items |
| `ng-click` | Handles click events |
| `ng-show` | Shows an element when expression is true |
| `ng-hide` | Hides an element when expression is true |
| `ng-disabled` | Enables/disables an HTML element |

---

## 13.1 `ng-app`

Defines the root of an AngularJS application and automatically bootstraps it.

```html
<div ng-app="myApp">
    ...
</div>
```

---

## 13.2 `ng-init`

Initializes application data.

```html
<div ng-app="" ng-init="name='John'">
    <p>{{name}}</p>
</div>
```

Output:

```text
John
```

> `ng-init` is useful for demonstrating initialization, although application data is commonly initialized in controllers.

---

## 13.3 `ng-model`

Creates/binds a model variable to an HTML control.

```html
<input type="text" ng-model="name">

<p>{{name}}</p>
```

The input and displayed value remain synchronized.

---

## 13.4 `ng-bind`

Binds AngularJS data to an HTML element.

```html
<p ng-bind="name"></p>
```

Equivalent idea:

```html
<p>{{name}}</p>
```

---

## 13.5 `ng-controller`

Associates a controller with a section of HTML.

```html
<div ng-app="myApp" ng-controller="myCtrl">
    {{name}}
</div>
```

---

## 13.6 `ng-repeat`

Repeats an HTML element for every item in a collection.

```html
<ul>
    <li ng-repeat="student in students">
        {{student.name}}
    </li>
</ul>
```

Example data:

```javascript
$scope.students = [
    {name: "Amit"},
    {name: "Rahul"},
    {name: "Neha"}
];
```

---

# 14. AngularJS Expressions

AngularJS expressions are written inside double curly braces:

```text
{{ expression }}
```

### Examples

#### Arithmetic

```html
<p>{{5 + 5}}</p>
```

Output:

```text
10
```

#### Variable

```html
<p>{{name}}</p>
```

#### Object

```html
<p>{{student.rollNo}}</p>
```

#### Array

```html
<p>{{marks[3]}}</p>
```

#### String combination

```html
<p>{{student.firstName + " " + student.lastName}}</p>
```

### Expressions vs JavaScript expressions

AngularJS expressions:

- Can contain literals, operators and variables.
- Can be written directly inside HTML.
- Support AngularJS filters.
- Do not support conditionals, loops and exceptions in the same way as normal JavaScript expressions.

---

# 15. Basic AngularJS Application Example

```html
<!DOCTYPE html>
<html>

<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>

<body>

<div ng-app="myApp" ng-controller="myCtrl">

    First Name:
    <input type="text" ng-model="firstName">

    <br>

    Last Name:
    <input type="text" ng-model="lastName">

    <br><br>

    Full Name: {{firstName + " " + lastName}}

</div>

<script>

var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});

</script>

</body>
</html>
```

### Working

```text
Input field
   ↓
ng-model
   ↓
$scope property
   ↓
AngularJS expression
   ↓
View updated
```

---

# 16. AngularJS Page Loading Process

When an AngularJS page loads:

1. Browser loads the HTML document.
2. AngularJS JavaScript file is loaded.
3. AngularJS creates its global object.
4. AngularJS scans the HTML for AngularJS applications/views.
5. The corresponding controller is connected to the view.
6. Controller functions execute.
7. Model data is populated.
8. AngularJS renders the view.
9. The page becomes ready.

---

# 17. AngularJS Filters

Filters transform or format data before displaying it.

### Common filters

| Filter | Purpose |
|---|---|
| `currency` | Formats a number as currency |
| `date` | Formats a date |
| `filter` | Selects matching items from an array |
| `json` | Converts/formats data as JSON |
| `limitTo` | Limits characters/elements |
| `lowercase` | Converts text to lowercase |
| `number` | Formats a number |
| `orderBy` | Sorts an array |
| `uppercase` | Converts text to uppercase |

### Filter syntax

```text
{{ value | filterName }}
```

### Example: uppercase

```html
<p>{{lastName | uppercase}}</p>
```

### Example: lowercase

```html
<p>{{lastName | lowercase}}</p>
```

### Example: currency

```html
<p>{{price | currency}}</p>
```

### Example: orderBy with `ng-repeat`

```html
<li ng-repeat="x in names | orderBy:'country'">
    {{x.name}}, {{x.country}}
</li>
```

### Example: filter an array

```html
<li ng-repeat="x in names | filter:'i'">
    {{x}}
</li>
```

This displays items containing the matching text.

---

# 18. Advantages of AngularJS

- Supports Single Page Applications.
- Provides two-way data binding.
- Reduces the amount of UI synchronization code.
- Supports dependency injection.
- Supports reusable components.
- Supports unit testing.
- Separates application responsibilities.
- Provides directives and filters for flexible UI development.
- Provides routing for SPA navigation.

---

# 19. Disadvantages / Limitations

The provided material lists:

- Client-side JavaScript alone cannot provide application security; server-side authentication and authorization are necessary.
- If JavaScript is disabled, the AngularJS application cannot function normally.
- Large/complex applications can become difficult to manage if AngularJS concepts are not organized properly.

---

# 20. Deep Linking

**Deep linking** means encoding the application state in the URL.

This allows a particular application state/view to be bookmarked and restored later.

Example:

```text
example.com/#!/student/101
```

The URL can represent a specific state/page of the application.

---

# 21. Routing

Routing means switching between different views/pages of an SPA without reloading the entire application.

AngularJS uses the `ngRoute` module for routing.

### Main components

- `ngRoute`
- `$routeProvider`
- `ng-view`

### Include route module

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular-route.js">
</script>
```

### Add dependency

```javascript
var app = angular.module("myApp", ["ngRoute"]);
```

### Configure routes

```javascript
app.config(function($routeProvider) {

    $routeProvider

    .when("/", {
        templateUrl: "main.htm"
    })

    .when("/red", {
        templateUrl: "red.htm"
    })

    .when("/green", {
        templateUrl: "green.htm"
    });

});
```

### View container

```html
<div ng-view></div>
```

`ng-view` is the placeholder where the selected route's template is displayed.

### Routing flow

```text
User clicks link
       ↓
URL changes
       ↓
$routeProvider finds matching route
       ↓
templateUrl selected
       ↓
Template loaded into ng-view
```

---

# Part 2 — AngularJS Services

## 22. What is an AngularJS Service?

An AngularJS **service** is a function or object available to an AngularJS application for performing reusable functionality.

AngularJS provides many built-in services.

Examples:

- `$location`
- `$http`
- `$timeout`
- `$interval`

Services are normally injected into controllers or other components through Dependency Injection.

### General pattern

```javascript
app.controller("myCtrl", function($scope, $http) {

});
```

Here `$http` is injected into the controller.

---

# 23. Why Use Services?

Services provide AngularJS-specific functionality and help keep application code modular and reusable.

For example, instead of directly using:

```javascript
window.location
```

AngularJS provides:

```javascript
$location
```

The provided material explains that AngularJS prefers its own service because AngularJS can properly supervise application changes and events.

---

# 24. `$location` Service

The `$location` service provides information about the current web page URL/location.

### Example

```javascript
var app = angular.module("myApp", []);

app.controller("customersCtrl", function($scope, $location) {

    $scope.myUrl = $location.absUrl();

});
```

### Important point

`$location` is passed into the controller as a dependency.

```text
Controller
   |
   +---- $scope
   |
   +---- $location
```

---

# 25. `$http` Service

`$http` is used to communicate with a server.

It can send HTTP requests and handle responses.

### GET example

```javascript
var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope, $http) {

    $http.get("welcome.htm")
        .then(function(response) {
            $scope.myWelcome = response.data;
        });

});
```

### Working

```text
AngularJS Controller
       |
       | $http.get()
       v
     Server
       |
       | Response
       v
response.data
       |
       v
$scope.myWelcome
       |
       v
     View
```

### Common HTTP operations

Conceptually:

```javascript
$http.get(url)
$http.post(url, data)
$http.put(url, data)
$http.delete(url)
```

The provided PDF specifically demonstrates `$http.get()`.

---

# 26. `$timeout` Service

`$timeout` is AngularJS's version of JavaScript's `setTimeout()`.

It executes a function after a specified delay.

### Example

```javascript
var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope, $timeout) {

    $scope.myHeader = "Hello World!";

    $timeout(function() {
        $scope.myHeader = "How are you today?";
    }, 2000);

});
```

`2000` milliseconds = `2` seconds.

### Use `$timeout` when

You need to execute something **once after a delay**.

---

# 27. `$interval` Service

`$interval` is AngularJS's version of JavaScript's `setInterval()`.

It repeatedly executes a function at a specified interval.

### Example

```javascript
var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope, $interval) {

    $scope.theTime = new Date().toLocaleTimeString();

    $interval(function() {
        $scope.theTime = new Date().toLocaleTimeString();
    }, 1000);

});
```

The function runs every `1000 ms` = `1 second`.

### Use `$interval` when

You need repeated execution after every fixed interval.

---

# 28. `$timeout` vs `$interval`

| `$timeout` | `$interval` |
|---|---|
| Executes after a delay | Executes repeatedly |
| Similar to `setTimeout()` | Similar to `setInterval()` |
| Normally used for one delayed execution | Used for repeated execution |
| Example: execute after 2 seconds | Example: update time every 1 second |

---

# 29. AngularJS Events

AngularJS provides directives for handling user/DOM events.

Important event directives:

- `ng-click`
- `ng-disabled`
- `ng-show`
- `ng-hide`

Other event listener directives listed in the material include:

```text
ng-blur
ng-change
ng-click
ng-copy
ng-cut
ng-dblclick
ng-focus
ng-keydown
ng-keypress
ng-keyup
ng-mousedown
ng-mouseenter
ng-mouseleave
ng-mousemove
ng-mouseover
ng-mouseup
ng-paste
```

---

# 30. `ng-click`

`ng-click` executes an expression/function when an element is clicked.

### Example

```html
<button ng-click="count = count + 1" ng-init="count=0">
    Increment
</button>

<div>Current Count: {{count}}</div>
```

Each click increases `count` by `1`.

---

# 31. `ng-disabled`

`ng-disabled` controls whether an HTML element is disabled.

### Example

```html
<div ng-app="" ng-init="mySwitch=true">

    <button ng-disabled="mySwitch">
        Click Me!
    </button>

    <input type="checkbox" ng-model="mySwitch">

</div>
```

### Working

```text
mySwitch = true
      ↓
button disabled

mySwitch = false
      ↓
button enabled
```

---

# 32. `ng-show`

`ng-show` displays an element when its expression evaluates to `true`.

### Example

```html
<button ng-click="show = true">
    Show Angular
</button>

<div ng-show="show">
    AngularJS
</div>
```

If:

```text
show = true
```

the element is visible.

If:

```text
show = false
```

the element is hidden.

---

# 33. `ng-hide`

`ng-hide` works opposite to `ng-show`.

The element is hidden when the expression is `true`.

```html
<div ng-hide="isHidden">
    AngularJS
</div>
```

### Difference

| `ng-show` | `ng-hide` |
|---|---|
| Shows when expression is `true` | Hides when expression is `true` |
| `true` → visible | `true` → hidden |
| `false` → hidden | `false` → visible |

---

# 34. AngularJS Forms

AngularJS forms provide:

- Data binding
- Input handling
- Client-side validation
- Form/input state tracking

Common controls:

- `input`
- `select`
- `button`
- `textarea`

---

# 35. Form Data Binding

Use `ng-model` to bind input controls to application data.

```html
<input type="text" ng-model="firstname">
```

Now `firstname` becomes available to the AngularJS application.

Example:

```javascript
app.controller("formCtrl", function($scope) {
    $scope.firstname = "ABCD";
});
```

---

# 36. Checkbox with `ng-model`

A checkbox generally has a boolean value:

```text
true / false
```

Example:

```html
<input type="checkbox" ng-model="myVar">

<h1 ng-show="myVar">
    My Header
</h1>
```

When the checkbox is checked:

```text
myVar = true
```

and the heading is shown.

---

# 37. Radio Buttons

Radio buttons can be bound using `ng-model`.

```html
<input type="radio"
       ng-model="myVar"
       value="dogs"> Dogs

<input type="radio"
       ng-model="myVar"
       value="cars"> Cars
```

Radio buttons with the same `ng-model` represent different values. The selected value is stored in the model.

---

# 38. Select Box

A select box can also use `ng-model`.

```html
<select ng-model="myVar">
    <option value="dogs">Dogs</option>
    <option value="tuts">Tutorials</option>
    <option value="cars">Cars</option>
</select>
```

The selected option's value is stored in `myVar`.

---

# 39. Form Reset

The provided material demonstrates using a master object and `angular.copy()` to reset form values.

```javascript
app.controller("formCtrl", function($scope) {

    $scope.master = {
        firstName: "Amit",
        lastName: "Jain"
    };

    $scope.reset = function() {
        $scope.user = angular.copy($scope.master);
    };

    $scope.reset();
});
```

### Why `angular.copy()`?

It creates a copy of the master object instead of simply pointing both variables to the same object.

---

# 40. AngularJS Form Validation

AngularJS provides client-side form validation.

AngularJS tracks whether form controls have been:

- Touched
- Modified
- Valid
- Invalid

### Important security point

Client-side validation is not sufficient for security.

**Server-side validation is also required.**

---

# 41. `required` Validation

```html
<form name="myForm">

    <input
        name="myInput"
        ng-model="myInput"
        required>

</form>

<p>{{myForm.myInput.$valid}}</p>
```

If the required field contains valid input:

```text
true
```

Otherwise:

```text
false
```

---

# 42. Email Validation

Use:

```html
<input
    name="myInput"
    ng-model="myInput"
    type="email">
```

AngularJS checks whether the value has a valid email format.

---

# 43. Form/Input States

AngularJS maintains different states for form controls.

| State | Meaning |
|---|---|
| `$untouched` | User has not touched the field |
| `$touched` | User has touched the field |
| `$pristine` | Field has not been modified |
| `$dirty` | Field has been modified |
| `$invalid` | Field value is invalid |
| `$valid` | Field value is valid |

These states are boolean properties.

---

# 44. AngularJS Validation CSS Classes

AngularJS automatically applies CSS classes according to control state.

| CSS class | Meaning |
|---|---|
| `ng-untouched` | Not touched |
| `ng-touched` | Touched |
| `ng-pristine` | Not modified |
| `ng-dirty` | Modified |
| `ng-valid` | Valid |
| `ng-invalid` | Invalid |
| `ng-valid-*` | Specific validation is valid |
| `ng-invalid-*` | Specific validation is invalid |

Example:

```text
ng-invalid-required
```

means the required validation has failed.

---

# 45. Accessing Form and Input Properties

### Form property

```text
<formName>.<property>
```

Example:

```javascript
myForm.$valid
```

### Input property

```text
<formName>.<inputName>.<property>
```

Example:

```javascript
myForm.myInput.$valid
```

---

# 46. Validation Directives

| Directive | Purpose |
|---|---|
| `ng-required` | Dynamically sets required |
| `ng-minlength` | Sets minimum length |
| `ng-maxlength` | Sets maximum length |
| `ng-pattern` | Validates using a regular expression |

Example:

```html
<input
    ng-model="username"
    ng-minlength="5"
    ng-maxlength="20">
```

Pattern example:

```html
<input
    ng-model="username"
    ng-pattern="/^[A-Za-z]+$/">
```

---

# 47. `$error`

`$error` contains validation information/errors for a form control.

Example:

```javascript
myForm.myInput.$error
```

It can be used to determine which validation rules have failed.

---

# 48. `ng-template`

`ng-template` is used to load the content of a `<script>` element into `$templateCache`.

The template can then be used by mechanisms such as:

- `ng-include`
- `ng-view`
- `template`
- Routing

### Important rule

The script type must be:

```html
type="text/ng-template"
```

and the template should have an `id`.

Example:

```html
<script type="text/ng-template" id="student.html">

    <h2>Student Details</h2>
    <p>{{student.name}}</p>

</script>
```

The `id` can be used as the template URL/reference.

---

# 49. `ng-options`

`ng-options` is used to generate options for a `<select>`/dropdown from an array.

Basic syntax:

```html
<select ng-options="arrayExpression">
</select>
```

Example:

```html
<select
    ng-model="selectedStudent"
    ng-options="student.name for student in students">
</select>
```

Optional initial option:

```html
<option value="">--Select--</option>
```

### `ng-options` vs `ng-repeat`

The provided material notes that `ng-options` can be more efficient for dropdown lists because it does not create a separate scope for every repeated option in the same way as `ng-repeat`.

---

# 50. Digest Cycle

The **digest cycle** is an important AngularJS mechanism responsible for detecting changes in watched values and updating the DOM.

### Basic process

```text
Application event
      ↓
Digest cycle
      ↓
Check watched values
      ↓
Compare current value with previous value
      ↓
Changes detected?
      ↓
Execute watch listeners
      ↓
Update DOM
      ↓
Browser displays updated UI
```

### Dirty checking

AngularJS compares the current value of a watched variable with its previous value.

This comparison is called **dirty checking**.

If a change is detected:

1. The relevant watch listener is executed.
2. AngularJS checks whether further values changed.
3. The DOM is updated after the digest process.

### Multiple iterations

The provided material explains that:

- At least two checking iterations can occur.
- More iterations may be required when one watch listener changes another value.
- The material states a maximum of 10 iterations before an error is thrown.
- Keeping digest work small is important for performance.

### Example concept

Suppose:

```text
Event changes b
    ↓
Digest checks b
    ↓
Listener changes c
    ↓
Digest checks c
    ↓
Listener changes a
    ↓
Another check
    ↓
No more changes
    ↓
DOM updated
```

---

# 51. Quick Revision — Important AngularJS Terms

| Term | One-line meaning |
|---|---|
| AngularJS | JavaScript framework for dynamic web applications |
| SPA | Application where views change without full page reload |
| Module | Container for AngularJS application components |
| Controller | Controls application/view data and logic |
| Scope | Object connecting controller and view |
| Model | Application data/state |
| View | User interface |
| ViewModel | Intermediate layer between Model and View |
| Directive | Extends HTML with AngularJS behavior |
| Expression | AngularJS expression written using `{{ }}` |
| Data Binding | Synchronization between model and view |
| Two-way Binding | Changes flow between model and view |
| Service | Reusable AngularJS functionality |
| Filter | Transforms/formats displayed data |
| Routing | Switching views without full page reload |
| `ng-view` | Container for routed views |
| `$routeProvider` | Configures application routes |
| `$http` | Communicates with a server |
| `$location` | Provides current URL/location information |
| `$timeout` | Executes code after a delay |
| `$interval` | Executes code repeatedly at intervals |
| Digest Cycle | Detects changes and updates the DOM |
| Dirty Checking | Comparing current and previous watched values |

---

# 52. Most Important Directives for Exams

```text
ng-app
ng-init
ng-model
ng-bind
ng-controller
ng-repeat
ng-click
ng-disabled
ng-show
ng-hide
ng-view
ng-options
ng-template
```

---

# 53. Most Important Services from the Provided Material

```text
$location
$http
$timeout
$interval
$routeProvider
```

---

# 54. Important Comparisons

## `ng-show` vs `ng-hide`

| `ng-show` | `ng-hide` |
|---|---|
| `true` → show | `true` → hide |
| `false` → hide | `false` → show |

## `$timeout` vs `$interval`

| `$timeout` | `$interval` |
|---|---|
| Delayed execution | Repeated execution |
| Similar to `setTimeout()` | Similar to `setInterval()` |
| Usually one delayed execution | Runs repeatedly |

## `ng-bind` vs `{{ }}`

| `ng-bind` | `{{ }}` |
|---|---|
| Attribute/directive syntax | Expression/interpolation syntax |
| `<p ng-bind="name"></p>` | `<p>{{name}}</p>` |
| Both display AngularJS data | Both display AngularJS data |

## `ng-repeat` vs `ng-options`

| `ng-repeat` | `ng-options` |
|---|---|
| Repeats HTML elements | Generates select/dropdown options |
| General-purpose collection repetition | Mainly used with `<select>` |
| Can create scopes for repeated instances | Material notes lower memory usage for dropdown generation |

---

# 55. Exam-Focused Flow to Remember

```text
AngularJS Application
        |
      Module
        |
   +----+----+----------------+
   |         |                |
Controller  Service          Filter
   |
 $scope
   |
 Data Binding
   |
   View
   |
Directives / Expressions
   |
 DOM
```

For SPA navigation:

```text
User
 ↓
Route
 ↓
$routeProvider
 ↓
templateUrl
 ↓
ng-view
 ↓
View
```

For server communication:

```text
Controller
 ↓
$http
 ↓
REST/Web Server
 ↓
Response
 ↓
$scope
 ↓
View
```

For data changes:

```text
User/Event
 ↓
$scope / Model changes
 ↓
Digest Cycle
 ↓
Dirty Checking
 ↓
Watch Listener
 ↓
DOM update
```
