# Models, Binding, Controllers and Scope

Lets start by creating the simplest possible Angular app.

```
<html>
  <head>
  </head>
  <body>
    <h1>Whats up, robbyronk?</h1>
  </body>
</html>
```
Replace robbyronk with your github name.

First, include the Angular JavaScript in the `<head>` tag.

```
<head>
  <script src="angular.js"></script>
</head>
```

Second, change the opening `<html>` tag to `<html ng-app>`.
Now we have an Angular app, but it doesnt do anything yet.
Lets have it do the addition for us. Replace your github name with
`{{'YourGithubName'}}`. Notice the single quotes.

```
<h1>Whats up, {{'robbyronk'}}</h1>
```

Refresh the page to see your app. Isnt that spectacular?

Lets make it do something.

Add the following line right below the `h1` tag, changing my name for your name.

```
<input type="text" ng-model="name" value="robbyronk">
```

Change the h1 tag like so:

```
<h1>Whats up, {{name}}?</h1>
```

Refresh the page and type your name in the input box.
You just made an interactive web page without writing any JavaScript!

Lets dive deeper into AngularJS and write some JS.

Open up a new file named "main.js". Type in this:

```
function MainController($scope) {
  $scope.name = 'robbyronk';
}
```

Great, now back in "index.html". Add this line right below the angular.js one.
`<script src="main.js"></script>`

Change the `<body>` tag to look like `<body ng-controller="MainController">`.

Now reload the page, you should see name prepopulated in both the input box and the
greeting. This is because the variable 'name' is 'in scope'. Scope is a complex subject
and we will talk much more about it. For now though, lets move on.

Change "main.js" to look like this.
```
function MainController($scope) {
  $scope.name = 'robbyronk';

  $scope.posts = [
    'The Internet is for Cats',
    'Kitties!',
    'I Wish Every Day was Caturday'
  ];
}
```

Add these lines just below the input box.

```
<div ng-repeat="post in posts">
  <h2>{{post}}</h2>
</div>
```

Refresh the page and look what you have! The controller puts an array of strings in
scope and in the HTML we can repeat a block for each string in the array. What we dont
see is all the scopes that are involved.

Insert this line in your `<head>` tag and refresh the page.
```
<style>.ng-scope { border: red 3px solid; }</style>
```

Each red box is an Angular scope. Some scope contain other scopes. In most cases, all
of the variables from the outer scope will be accessible from the inner scopes. We will
see special cases later where the inner scopes get isolated from the outer scope. Lets
see this outer-inner relationship first hand though.

Add this line below the `<h2>` line.
```
<p>posted by {{name}}</p>
```

Refresh and you should see your name on each post. Try changing the name in the input box.
See how all of the names change? Thats because name is from the outer scope and changes
to it are reflected to the inner scopes.
