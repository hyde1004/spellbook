#### YAML 사용하기

###### Reference
 - [Struggling With Ruby](http://strugglingwithruby.blogspot.kr/2008/10/yaml.html?m=1)
 - [YAML - Data Serialization in Ruby](http://csc.columbusstate.edu/woolbright/class/swatson.pdf)

YAML은 XML에 비해 눈으로 데이터 확인이 용이하며, 해당 데이터를 쉽게 직렬화할 수 있다.

다음은 YAML의 hello program이다.

```ruby
-
  name: Tom
  age: 32
-
  name: Dick
  age: 19  
EOS

config = YAML.load(yaml_string)	# from yaml_string

puts config[0]['age']  # 32
puts config[1]['name'] # Dick
```

YAML을 구성하기 위해서는 Array 로 할것인가, Hash로 할것인가로 결정해주면 된다. 물론 중첩도 가능하다.
```ruby
arry = <<EOS
- [Tom, 32] # Array
- [Dick, 19] # Array
EOS

hash = <<EOS
{ name: Tom, age:32 } # Hash
EOS
```

다음은 기본적인 사용법을 정리한 hello_yaml.rb 이다.
```ruby
# 필요한 파일
require 'yaml'

# 변환
str = "Hello, Yaml!"
puts str.to_yaml # y(str)


arr = ["one", "two", "three"]
puts arr.to_yaml # y(arr)

# 파일 저장
fileName = File.open('counting.yml', 'w')
	YAML.dump(arr, fileName)
fileName.close

# 파일 읽기
fileName = File.open('counting.yml', "r")
	newArr = YAML.load(fileName) # to array
fileName.close

puts newArr.to_yaml # y(newArr)
```