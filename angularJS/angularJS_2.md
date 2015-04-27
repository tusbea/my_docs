`index.html`로 들어가면 자동으로 `index.html#/home`로 이동한다.  
`<a href="#/register">register</a>` 링크를 클릭하면 `index.html#

```js
// app.js
var App = angular.module("myApp", []);

App.controller('myController', function($scope) {
	$scope.people = [
		{name: 'john', city: 'yrance'},
		{name: 'jimmy', city: 'newyork'},
		{name: 'Tom', city: 'italy'}
	];

	$scope.add = function() {
		$scope.people.push( {name: $scope.NewPerson.name, city: $scope.NewPerson.city} )
	};
});

App.config(function($routeProvider) {
	$routeProvider
		.when('/home', {
			controller : 'myController',
			templateUrl : 'templates/home.html'
		})
		.when('/register', {
			controller : 'myController',
			templateUrl : 'templates/register.html'
		})
		.otherwise({
			redirectTo : '/home'
		});
});
```

angularjs 버전이 높으면 라우팅이 안되는 경우가 있다.

```html
<!-- index.html -->
<html ng-app="myApp">

<head>
	<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js"></script>
	<script src="app.js"></script>
</head>

<body>
	<div ng-view></div>
</body>

</html>
```

```html
<!-- templates/home.html -->
<div>
	<ul> 
		<li ng-repeat="person in people | orderBy: 'city'">
		{{ person.name | uppercase }} - {{ person.city }}</li>
	</ul>

	Name:
	<br />
	<input type="text" ng-model="NewPerson.name" /> 
	<br />
	City:
	<br />
	<input type="text" ng-model="NewPerson.city" /> 
	<br />
	<button ng-click="add()">add</button>
	<br />
	<a href="#/register">register</a>
</div>
```

```html
<!-- templates/register.html -->
<html>
	<title>register</title>
</html>
```