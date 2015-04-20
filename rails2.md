원문 : http://guides.rubyonrails.org/action_controller_overview.html

## 1. What Does a Controller Do?

routing -> determine controller -> produce the appropriate output

receive request -> fetch or save data from a model -> use a view to create HTML output

## 2. Controller Naming Convention

{name}Controller  
{name}에는 보통 복수형이 들어간다.  
e.g. ClientsController

이 방법을 사용하면 default route generators(e.g. resources)로 생성된 라우팅 규칙을 그대로 쓸 수 있다.

	model은 controller와 달리 단수형을 사용한다.

## 3. Methods and Actions

controller는 `ApplicationController`를 상속하는 클래스이다.  
라우팅이 끝나면 어떤 controller의 어떤 action이 실행될지 결정된다.

다음의 컨트롤러에서 new 액션이 실행되면 기본으로 new.html.erb를 render한다.

~~~ruby
class ClientsController < ApplicationController
  def new
  end
end
~~~

<br>
`ApplicationController`는 `ActionController::Base`를 상속한다.  

## 4. Parameters

Rails에는 2가지 parameter가 있다. 2가지 방식의 parameter는 Rails에서 처리될 때 차이가 없다.  

1. part of the URL. query string parameters
	* URL의 ? 뒤에 따라오는 string
2. POST data
	* HTML form에 입력된 값들

parameter는 `params` 변수에 해시 형태로 전달된다.

~~~ruby
class ClientsController < ApplicationController
  def index
    if params[:status] == "activated"
    ...
  end
  
  def create
    @client = Client.new(params[:client])
    ...
  end
end
~~~

### 4.1 Hash and Array Parameters

`params`로 배열도 보낼 수 있다. 다음과 같이 요청하면 `params[:ids]`에는 배열이 저장된다.  
parameter로 전달되는 것들은 모두 string이다.

~~~a
GET /clients?ids[]=1&ids[]=2&ids[]=3
~~~
	
~~~ruby
params[:ids] = ["1", "2", "3"]
~~~

URL에는 [, ]가 들어갈 수 없어서 실제 전달되는 URL은 아래와 같다. 보통은 브라우저와 Rails가 알아서 encode, decode를 한다. 만약 직접 요청할 경우에는 다음과 같이 직접 encode하여 전달해야 한다.

~~~a
GET /clients?ids%5b%5d=1&ids%5b%5d=2&ids%5b%5d=3
~~~

다음과 같은 form을 submit하면 전달되는 `params`는 아래와 같다.  
참고로 `input` form 중에서 name 속성이 지정된 값들만 parameter로 전달된다. 

~~~html
<form accept-charset="UTF-8" action="/clients" method="post">
  <input type="text" name="client[name]" value="Acme" />
  <input type="text" name="client[phone]" value="12345" />
  <input type="text" name="client[address][postcode]" value="12345" />
  <input type="text" name="client[address][city]" value="Carrot City" />
</form>
~~~

~~~ruby
params[:client] = { 
  "name" => "Acme", 
  "phone" => "12345", 
  "address" => { "postcode" => "12345", "city" => "Carrot City" } 
}
~~~

`params`는 `ActiveSupport::HashWithIndifferentAccess`의 인스턴스이다. 이 인스턴스는 해시와 비슷하지만 key로 string과 symbol을 섞어서 사용할 수 있다.

### 4.2 JSON parameters

request가 `Content-Type: Application/json`일 때 Rails는 자동으로 JSON content를 `params`로 변환한다.  
다음은 JSON content의 예이다.

~~~json
{ "company": { "name": "acme", "address": "123 Carrot Street" } }
~~~
	
### 4.3 Routing Parameters

다음과 같은 라우팅 규칙이 있다고 가정하자. 유저가 /clients/active URL을 열면 `params` 해시 값은 그 아래와 같다.

~~~a
get '/clients/:status' => 'clients#index', foo: 'bar'
~~~

~~~ruby
params[:status]		# "active"
params[:foo]		# "bar"
~~~

아래와 같이 `params`에는 `:action` key에 대한 값도 존재한다. 마찬가지로 컨트롤러에 대한 값도 저장되지만 해시로 직접 접근하기보다는 `controller_name`, `action_name` 메소드를 이용하는 것이 좋다.

~~~ruby
params[:action]		# "index"
~~~

### 4.5 Strong Parameters

whitelist : 받아들일 key를 지정하는 과정

Active Model mass assignment : 다음 코드처럼 whitelisting 과정을 거치지 않고 `params`를 전달하는 코드

~~~ruby
Person.create(params[:person])
~~~

exception이 발생하면 `ActionController::Base`에서 catch하고 400 Bad Request를 reply한다.  
따라서 `params`를 사용할 때는 다음과 같이 whitelisting 과정을 거쳐야 한다.

~~~ruby
params.require(:person).permit(:name, :age)
~~~

#### 4.5.1 Permitted Scalar Values

다음과 같은 코드는 `params`의 `:id` key만 whitelisting한다. 이 때의 value는 스칼라(not array, hash, object) 값이어야 한다.

~~~ruby
params.permit(:id)
~~~

만약 array, hash 등을 허용하려면 다음과 같이 코드를 작성한다.

~~~ruby
params.permit(id: [])
~~~

모든 해시를 허용하려면 `permit!` 메서드를 사용한다. 다음 코드에서는 `:log_entry` 해시와 그 sub-hash들을 모두 허용한다.

~~~ruby
params.require(:log_entry).permit!
~~~

#### 4.5.2 Nested Parameters

다음 코드는 name, emails, friends 속성을 whitelisting한다.

~~~ruby
params.permit(
  :name, 
  { emails: [] },
  friends: [ 
    :name,
    { family: [ :name ], hobbies: [] }])
~~~

