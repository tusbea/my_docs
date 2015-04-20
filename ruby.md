# Chapter 1

## Data Types
Numbers, Strings, Booleans  

~~~ruby
my_num = 3
my_boolean = false
my_string = "hello"
~~~

## Math

~~~ruby
a = 1 + 2
b = 1 - 2
c = 1 * 2
d = 1 / 2
e = 1 ** 2
f = 1 % 2
~~~

## puts, print

~~~ruby
puts "hello"		# 출력한 뒤에 newline
print "hello"		# 출력만 한다.
~~~

## String Method

~~~ruby
"I love you".length		# 10
"Eric".reverse			# "cirE"
"eric".upcase			# "ERIC"
"ERIC".downcase			# "eric"
"eRiC".capitalize		# "Eric"
name = "kim"
name.capitalize!		# 느낌표를 붙이면 변수 자체를 capitalize한다.
~~~

## Comment

~~~ruby
# single line comment
=beign
multiline comment
=end
~~~

## Naming Conventions

~~~ruby
my_num = 1		# 보통 변수는 왼쪽과 같이 이름을 정한다.
~~~

# Chapter 2

## gets

~~~ruby
x1 = gets			# 입력을 받는다.
x2 = gets.chomp		# gets는 뒤에 \n이 붙지만 chomp를 붙이면 \n을 없앤다.
~~~

## String Interpolation

~~~ruby
first_name = "Kevin"
puts "your name is #{first_name}"
~~~

# Chapter 3

## if, elsif, else

~~~ruby
if x < y
	...
elsif x = y
	...
else
	...
end
~~~

## unless

~~~ruby
unless x < y
	...
else
	...
end
~~~

## comparator

문장의 결과에 따라 true 또는 false를 리턴한다.

~~~ruby
x == y
x != y
x < y
x <= y
x > y
x >= y
~~~

## and, or, not

~~~ruby
true && true
false || true
!true
~~~

# Chapter 4

## String Methods

~~~ruby
if string.include? "substring"
	...
end

"apple".gsub("a", "b")		# "bpple"

"i am kim".split(" ")		# ["i", "am", "kim"]
~~~

# Chapter 5

## while

~~~ruby
while i < 5
	...
end
~~~

## until

~~~ruby
until i == 6
	...
end
~~~

## Assignment Operators

~~~ruby
a += 1
b -= 1
~~~

## for

~~~ruby
for num in 1...10		# 1 ~ 9. 10을 포함하려면 1..10처럼 점을 2개 사용한다.
	puts num
end
~~~

## loop

~~~ruby
loop { ... }		# infinite loop

loop do
	...
	break if i > 5		# break는 루프를 빠져나오는 키워드
	next if i % 2 == 1	# 다음 step으로 넘어가는 키워드
end
~~~

## array

~~~ruby
my_array = [1,2,3,4]
~~~

## .each Iterator

~~~ruby
my_array = [1,2,3,4]

my_array.each { |i| puts i }

my_array.each do |i|
	puts i
end
~~~

## .times Iterator

~~~ruby
10.times do		# 10번 실행
	...
end
~~~

# Chapter 6

## array

~~~ruby
array = [1,2,3,4,5]
puts array[1]		# 2
~~~

## hash

~~~ruby
hash = {
	"key1" => 1,
	"key2" => 2
}

my_hash = Hash.new		# 새로운 empty hash 생성
my_hash["key3"] = 3		# 새로운 key, value 추가
new_hash = Hash.new(0)	# 저장되지 않은 key에 대해 접근하면 default 값이 0이 된다.
~~~

## Iteration over array/hash

~~~ruby
# 배열 반복
numbers = [1, 2, 3, 4, 5]
numbers.each { |e| puts e }

# 해시 반복
menu = {
	"apple" => 1,
	"banana" => 2
}
menu.each do |k, v|
	puts "#{k}, #{v}"
end
~~~

## Sorting the Hash

~~~ruby
colors = {
	"blue" => 3,
	"yellow" => 1,
	"purple" => 2
}
# count 값에 따라 오름차순 정렬
colors = colors.sort_by { |_, count| count }
~~~

## Compare Operator

a <=> b : a가 b보다 순서상 앞이면 -1, 뒤면 1, 동일 순서이면 0을 리턴한다.

~~~ruby
1 <=> 2			# -1. 1이 2보다 순서상 앞이므로
"abc" <=> "aa"	# 1. "abc"가 순서상 "aa"보다 뒤이므로
~~~

# Chapter 7

## Methods

~~~ruby
def foo(a, b)		# def foo a, b <- 괄호 생략 가능
	puts a, b
	return a + b	# return을 하지 않으면 마지막 문장의 값이 리턴된다.
end
~~~

## splat arguments(복수개의 argument)

~~~ruby
def what_up(greeting, *bros)		# 여러 개의 argument를 bros에 저장
	brow.each { |bro| puts "#{greeting}, #{bro}!" }
end

what_up("What up", "John", "Park", "Kim")
~~~

## Blocks = Nameless Methods

do, end 또는 {, }로 둘러싸인 부분은 이름없는 함수와 비슷하다.

# Chapter 8

## nil

존재하지 않는 key에 대해 해시를 접근하면 nil을 반환한다. nil은 false와 함께 non-true를 의미한다. 그 이외의 값들은 모두 true를 의미한다.

~~~ruby
if 2		# if true
	...
end
~~~

## symbol

symbol은 일종의 이름이라고 생각할 수 있다. symbol은 string이 아니다.  
string은 같은 값이더라도 동시에 2개 이상이 존재할 수 있지만, symbol은 동시에 1개만 존재한다.  
symbol은 보통 해시의 key 또는 메소드 이름을 가리킬 때 사용된다.

~~~ruby
:string != "string"
~~~

## symbol <-> string

~~~ruby
:apple.to_s		# "apple"
"apple".to_sym	# :apple
"apple".intern	# :apple. string to symbol의 또 다른 방법
~~~

## 새로운 해시 정의 방법

다음의 두 해시는 같은 해시이다.

~~~ruby
new_hash = {
	one: 1,
	two: 2
}

old_hash = {
	:one => 1,
	:two => 2
}
~~~

## 해시 select

~~~ruby
grades = {
	alice: 100,
	bob: 92,
	dave: 97
}

# grade < 97인 key, value만 취한 해시를 리턴한다.
grades.select ( |name, grade| grade < 97 }
~~~

## 해시 iterate(key, value)

~~~ruby
my_hash = { one: 1, two: 2 }
my_hash.each_key { |k| puts k }
my_hash.each_value { |v| puts v }
~~~

# Chapter 9

## case

~~~ruby
case language
when "JS"
	...
when "Python"
	...
else
	...
end

# 다음과 같이 한 줄로 작성할 수도 있다.
case language
	when "JS" then ...
	...
end
~~~

## conditional Assignment

~~~ruby
book = nil
book ||= "hello"		# book = "hello"
book ||= "hi"			# book = "hello". book에 이미 값이 있으므로 "hi"는 할당되지 않는다.
~~~

## iteration

~~~ruby
95.upto(100) { |n| print n, " " }		# 95 96 97 98 99 100
100.downto(95) ...
~~~

## call and response

~~~ruby
[1,2,3].respond_to?(:push)		# push method를 호출할 수 있는가
~~~

## <<

~~~ruby
[1,2,3] << 4			# [1,2,3,4]
"hello" << " world"		# "hello world"
"hello" + " world"		# 위와 같음
~~~

# Chatper 10

## collect Method

~~~ruby
my_nums = [1,2,3]
my_nums.collect { |n| n **2 }		# [1,4,9]
~~~

## yield keyword

~~~ruby
def foo
	...
	yield
	...
end

foo { ... }		# foo 함수의 yield 부분에서 block이 실행된다.
~~~

## yield with parameters

~~~ruby
def foo
	...
	yield(1)
	...
end

foo { |n| puts n }		# yield의 parameter 1이 n으로 전달되어 실행된다.
~~~

## block을 object로 저장하기

ruby에서 거의 대부분은 object이다. 하지만 block은 object가 아니다.  
Proc을 이용하여 block을 object로 저장할 수 있다.

~~~ruby
cube = Proc.new { |n| n ** 3 }
[1,2,3].collect(&cube)		# &는 Proc을 block으로 변환한다.
~~~

## proc 호출

~~~ruby
hi = Proc.new { puts "hello" }
hi.call		# hi proc 실행
~~~

## symbol을 block으로 변환

&:to_i : &를 통해 symbol을 block으로 변환한다.

~~~ruby
strings = ["1", "2", "3"]
strings.map &:to_i			# strings.map { |x| x.to_i }
~~~

## lambda

약간의 차이를 제외하고 proc과 유사하다.  
첫번째로 argument passing 방식에서 차이가 있다. lambda는 argument 개수가 다르면 error를 throw하지만, proc은 모자란 argument는 nil로 채우고 남는 argument는 무시한다.  
두번째로 lambda는 리턴하면 호출한 곳으로 이동하지만, proc은 리턴하면 그대로 리턴을 한다.

~~~ruby
strings = ["hello", "hi"]
symbolize = lambda { |x| x.to_sym }
strings.collect &symbolize
~~~
