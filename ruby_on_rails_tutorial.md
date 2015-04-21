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

## testing

