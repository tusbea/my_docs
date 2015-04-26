Link : https://thinkster.io/angular-rails/

[TOC]

---

# Introduction

AngularJS : frontend  
Rails : build a JSON REST API

## Prerequisites

knowledge

* JavaScript
* Ruby

need

* Node.js
* npm

# Jumping in with Angular

AngularJS : frontend framework developed by Google

## Getting Started

아래 javascript 코드에서 만든 변수 `test`를 `{{ }}`를 이용하여 접근한다.

~~~html
<!-- index.html -->
<html>
  <head>
    <title>My Angular App!</title>
    <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.2.19/angular.min.js"></script>
    <script src="app.js"></script>
  </head>
  <body ng-app="flapperNews" ng-controller="MainCtrl">
    <div>
      {{test}}
    </div>
  </body>
</html>
~~~

`test` 변수를 생성한다.

~~~js
// app.js
angular.module('flapperNews', [])
.controller('MainCtrl', [
'$scope',
function($scope){
  $scope.test = 'Hello world!';
}]);
~~~

## Displaying Lists

AngularJS에서 리스트를 생성한다.

~~~js
$scope.posts = [
  'post 1',
  'post 2',
  'post 3',
  'post 4',
  'post 5'
];
~~~

html에서 위에서 정의한 리스트를 나열한다.

~~~html
<div ng-repeat="post in posts">
  {{post}}
</div>
~~~

ruby의 해시와 같은 데이터도 변수로 지정할 수 있다.

~~~js
$scope.posts = [
  {title: 'post 1', upvotes: 5},
  {title: 'post 2', upvotes: 2},
  {title: 'post 3', upvotes: 15},
  {title: 'post 4', upvotes: 9},
  {title: 'post 5', upvotes: 4}
];
~~~

해시의 각 attribute에 접근하는 방법은 다음과 같다.

~~~html
<div ng-repeat="post in posts">
  {{post.title}} - upvotes: {{post.upvotes}}
</div>
~~~

정렬하려면 다음과 같이 `orderBy` 필터를 사용한다.

~~~html
<div ng-repeat:"post in posts | orderBy: '-upvotes': true">
  {{post.title}} - upvotes: {{post.upvotes}}
</div>
~~~

# Getting User Input

