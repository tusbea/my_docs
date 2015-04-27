## 방법

1. `Gemfile`에 다음 라인 추가

	```
	gem 'rspec-rails', :group => [:development, :test]
	gem 'simplecov', :require => false, :group => :test
	```

2. `$ bundle install`
3. `$ rails g rspec:install`
4. `spec/spec_helper.rb`에 다음 라인 추가

	```
	require 'simplecov'

	SimpleCov.start do
		add_filter '/spec/'
		add_filter '/config/'
		add_filter '/lib/'
		add_filter '/vender/'

		add_group 'Controllers', 'app/controllers'
		add_group 'Models', 'app/models'
		add_group 'Helpers', 'app/helpers'
		add_group 'Mailers', 'app/mailers'
		add_group 'Views', 'app/views'
	end
	```
	
## spec 파일 생성 방법

```
$ rails g rspec:controller application
$ rails g rspec:model user
```

환경 설정 후에는 controller나 model 생성시 spec 파일도 자동으로 생성된다.