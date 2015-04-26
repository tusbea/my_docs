http://www.w3schools.com/angular/

AngularJS is a JavaScript framework.

html 파일의 head 부분에 다음과 같이 작성하여 AngularJS를 사용할 수 있다.

~~~html
<head>
<script 
src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js">
</script>
</head>
~~~

## ng-directives

`ng-app` : AngularJS app이라고 알려준다.  
`ng-model` : HTML control(input, select)의 value를 application data로 binding한다.  
`ng-bind` : application data를 HTML view로 binding한다.

~~~html
<div ng-app="">
  <p>Name: <input type="text" ng-model="name"></p>
  <p ng-bind="name"></p>
</div>
~~~

## example

~~~html
<div ng-app="" ng-init="firstName='John'">
<p>The name is <span ng-bind="firstName"></span></p>
</div>
~~~

~~~html
<div data-ng-app="" data-ng-init="firstName='John'">
<p>The name is <span data-ng-bind="firstName"></span></p>
</div>
~~~

## AngularJS Expressions

written inside double braces: {{ expression }}

~~~html
<div ng-app="">
  <p>My first expression: {{ 5 + 5 }}</p>
</div>
~~~

다음 두 문장은 같은 의미이다.

~~~html
<p ng-bind="name"></p>
<p>{{name}}</p>
~~~

## AngularJS Applications

AngularJS modules : define AngularJS Applications  
AngularJS controllers : control AngularJS applications  

~~~html
<div ng-app="myApp" ng-controller="myCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
<br>
Full Name: {{firstName + " " + lastName}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstName= "John";
    $scope.lastName= "Doe";
});
</script>
~~~