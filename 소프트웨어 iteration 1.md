# 소프트웨어 제출할 것들
(due : 월요일 6시)

* specification update
* Design and Plan
	* github 위키 사용 
* short progress report
* coverage >= 70%
* Instructions for your TA to be able to check out a tagged version of the code that constitutes your iteration release.  
* A url and instructions for using the app in the current stage.  

## revised specification 

* 변경된 부분과 원래 내용은 다른 색으로
* 다음 iteration에서 만들 feature를 작성한다. 전체 iteration에 대해서도 대략적인 feature를 구상한다. 나중에 수정해도 된다.
* 다음 iteration의 feature를 미리 작성해야 하나?

## Design and Plan

* System Architecture
	* the major pieces and how they fit together
	* 되도록 그래픽으로 나타내기(UML)
	* component간의 interface
* Design Details
	* critical algorithms, protocols, key invariants
	* component간의 API 정도는 표현해야 한다.(처음부터 완벽할 필요는 없음)
	* client와 server간에 message가 전달된다면 그것(message, data, format)도 포함해야 함
	* 현재 iteration은 자세하게, future iteration은 간단히
* Implementation Plan
	* requirements의 user story를 쪼개서 프로그래밍 단위로 나누기(난이도, dependency 등을 고려)
* Testing Plan
	* 어떻게 테스트할 것인지. 다음 3가지로 나누어서 작성
		* unit testing
		* functional testing
		* acceptance & integration testing

## iteration progress report

* main difficulties
* implement하지 못한 내용들과 하지 못한 이유. 다음 iteration에 다시 할 것인지?
* test coverage, 어떤 부분을 테스트하고 테스트하지 않았는지
* test coverage 70% 이상. 스크린샷 포함
	* overall coverage
	* 가장 coverage가 낮은 클래스. 낮은 이유와 앞으로 그 클래스의 테스트를 어떻게 할건지
* 팀원들의 기여도
* Tag a branch or revision in your repository to identify the code you want to submit for iterationN (replace N with 1, 2, ...). The date and time of this revision should be before the deadline. This branch should include a README file with instructions on how to run the application and tests. 

## Features for 1st iteration

* sign up
* delete user
* sign in
* sign out
* view course index
* view a course
* create a course
* view profile
* edit profile
* ~~markdown~~