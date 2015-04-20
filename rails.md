# render, redirect_to
[Layouts and Rendering in Rails](http://guides.rubyonrails.org/layouts_and_rendering.html)

## Creating Responses

* `render`
* `redirect_to`  
* `head`

## render

`render` method : send a response back to the browser

#### 1. Rendering Nothing

~~~ruby
render nothing: true
~~~

#### 2. Rendering an Action's View
same controller, different template

~~~ruby
render "edit"
~~~

~~~ruby
render :edit
~~~

~~~ruby
render action: :edit
~~~

#### 3. Rendering an Action's Template from Another Controller
app/views를 기준으로 상대 경로를 지정하면 해당 템플릿을 render할 수 있다.

~~~ruby
render "products/show"
~~~

~~~ruby
render template: "products/show"
~~~

#### 4. Rendering Text

~~~ruby
render plain: "OK"
~~~

#### 5. Rendering JSON
object의 `to_json` 메소드를 호출할 필요 없다. `:json` 옵션을 주면 자동으로 해당 메소드를 호출한다.

~~~ruby
render json: @product
~~~

## redirect_to

`render` 메소드는 view를 렌더링하여 브라우저에게 전달한다. 따라서 컨트롤러에서 정의한 action 코드들은 실행되지 않는다.  
`redirect_to` 메소드는 브라우저에게 특정 action을 다시 요청하라고 말한다. 따라서 컨트롤러의 action 코드도 실행된다.

# Active Record Basics
[Active Record Basics](http://guides.rubyonrails.org/active_record_basics.html)

## Convention over Configuration

If you follow the conventions adopted by Rails, you'll need to write very little configuration

## Naming Conventions

Model/Class | Table/Schema
------------|--------------
Article     | articles
LineItem    | line_itmes

## CRUD

#### 1. Create
`create` 메서드는 오브젝트를 만들고 db에 저장한다.  
`new` 메서드는 오브젝트를 만들기만 한다.

~~~ruby
user = User.create(name: "David", occupation: "Code Artist")
~~~

~~~ruby
user = User.new
user.name = "David"
user.occupation = "Code Artist"
user.save		# 이 과정이 있어야 db에 저장된다.
~~~

~~~ruby
user = User.new do |u|
	u.name = "David"
	u.occupation = "Code Artist"
end
~~~

#### 2. Read

~~~ruby
users = User.all
user = User.first
# return the first user
david = User.find_by(name: "David")	
# find all users
users = User.where(name: "David", occupation: "Code Artist").order("created_at DESC")
~~~

#### 3. Update

~~~ruby
user = User.find_by(name: "David")
user.name = "Dave"
user.save
~~~

~~~ruby
user = User.find_by(name: "David")
user.update(name: "Dave")
~~~

#### 4. Delete

~~~ruby
user = User.find_by(name: "David")
user.destory
~~~

## Validations

`save` 또는 `update` 메서드를 호출할 때 내부적으로 validation 과정을 거친다. validation을 통과해야만 해당 메서드가 정상적으로 종료된다.  
`save!`, `update!` 메서드는 validation이 실패하면 `ActiveRecord::RecordInvalid` 예외를 발생시킨다.

~~~ruby
class User < ActiveRecord::Base
	validates :name, presence: true
end
 
user = User.new
user.save  # => false
user.save! # => ActiveRecord::RecordInvalid: Validation failed: Name can't be blank
~~~

## Migrations

rails에서는 migration을 통해 db schema를 관리한다.

~~~ruby
class CreatePublications < ActiveRecord::Migration
  def change
    create_table :publications do |t|
      t.string :title
      t.text :description
      ...
  end
end
~~~

`rake db:migrate` : 실제 테이블을 생성한다.
`rake db:rollback` : 테이블을 roll back한다.  
     
  
  
***
***

## .html.erb 주석

~~~ruby
<% if false %>
	code to comment
<% end %>
~~~

## heroku에서 postgresql 사용하기

config/database.yml 파일에서 username:user 추가  
`heroku rake db:migrate` 실행

## 특정 테이블 data 모두 삭제

~~~sh
$ rails console
> ModelName.delete_all
~~~

