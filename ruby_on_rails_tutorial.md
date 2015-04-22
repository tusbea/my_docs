## 단축 명령

Full Command | Shortcut
-------------|---------
`$ rails server` | `$ rails s`
`$ rails console` | `$ rails c`
`$ rails generate` | `$ rails g`
`$ bundle install` | `$ bundle`
`$ rake test` | `$ rake`


## Undoing things

`$ rails destroy` 명령을 사용하면 `$ rails generate`로 만든 파일들을 제거하고 수정된 파일들(routes.rb)을 되돌릴 수 있다.

~~~sh
$ rails generate controller StaticPages home help
$ rails destroy  controller StaticPages home help
~~~

컨트롤러와 마찬가지로 모델도 제거할 수 있다.

~~~sh
$ rails generate model User name:string email:string
$ rails destroy model User
~~~

migration도 되돌릴 수 있다. 세번째 명령은 db를 가장 처음으로 되돌린다. version은 migration할 때마다 1씩 증가하므로 버전 0은 처음 상태를 가리킨다.

~~~sh
$ bundle exec rake db:migrate
$ bundle exec rake db:rollback
$ bundle exec rake db:migrate VERSION=0
~~~

## 컨트롤러 생성

	$ rails generate controller StaticPages home help
	
이 명령을 실행하면 StaticPagesController를 만들고 home, help action을 추가한다.  
<br>
또한 `config/routes.rb` 파일에 다음 라인을 추가한다.

~~~ruby
Rails.application.route.draw do
  get 'static_pages/home'
  get 'static_pages/help'
  ...
end
~~~

여기서 `get 'static_pages/home'` 문장을 살펴보자. 이 문장은 GET request로 /static_pages/home URL 요청을 받으면 `StaticPagesController`의 `home` action을 실행한다는 의미이다.

~~~ruby
def home
end
~~~

`home` action에 아무런 코드가 없으면 해당 action이 실행될 때 자동으로 home.html.erb를 render한다.

## GET

GET : get a page  
POST : submit a form. 무언가를 만들 때 사용된다.  
PATCH : update things  
DELETE : delete things  
<br>
PATCH, DELETE는 브라우저가 natively 지원하지 않아서, GET, POST가 많이 사용된다.



# Chapter 4

## Rails-flavored Ruby  

Chapter 4에서는 Ruby 언어 중에서 Rails에서 필요한 문법을 배운다.

## 4.1 Motivation

다음은 `app/views/layouts/application.html.erb` 파일이다.

~~~ruby
<%= stylesheet_link_tag 'application', media: 'all', 
  'data-turbolinks-track' => true %>
~~~

`stylesheet_link_tag`는 rails 함수이다. 이 함수는 `application.css`를 stylesheet로 지정한다.  
이 라인에는 4가지 문법사항이 있다.  

* built-in rails method
* method invocation with missing paranthesis
* symbol
* hash

## 4.2 Strings and methods

다음 코드의 2번째 라인과 3번째 라인은 같은 의미이다.

~~~ruby
%w[a b c]		# ["a", "b", "c"]
%w[a b c].map { |c| c.upcase }
%w[a b c].map(&:upcase)
~~~

## 4.3.4 CSS revisited

함수를 호출할 때 소괄호는 생략할 수 있다. 따라서 다음 두 문장은 같은 의미이다.

~~~ruby
stylesheet_link_tag('application', media: 'all',
  'data-turbolinks-track' => true)
stylesheet_link_tag 'application', media: 'all',
  'data-turbolinks-track' => true
~~~

또한 함수를 호출할 때 해시가 마지막 인자로 전달되면 중괄호를 생략할 수 있다. 따라서 다음 두 문장은 같은 의미이다.

~~~ruby
stylesheet_link_tag 'application', { media: 'all',
  'data-turbolinks-track' => true }
stylesheet_link_tag 'application', media: 'all',
  'data-turbolinks-track' => true
~~~

다음 문장에서 해시에서 심볼 대신 string을 사용한 이유는 중간에 하이픈(-)이 들어가면 심볼로 지정할 수 없기 때문이다.

~~~ruby
<%= stylesheet_link_tag 'application', media: 'all', 
  'data-turbolinks-track' => true %>
~~~

