[TOC]

## 참고할 사이트

* https://www.atlassian.com/git/tutorials/syncing/git-remote

## 개념

index = stagin area  
working directory : 실제 디렉토리

## git reset

이전 commit 상태로 되돌리기

~~~sh
git reset --hard HEAD
~~~

## git add

`git add -A`는 `git add .; git add -u`와 같다.

~~~sh
git add -A		# git add --all
git add -u		# git add -update
~~~

## git rebase

`git rebase`는 `git merge`와 비슷하다.  
`master` 브랜치와 `topic` 브랜치를 rebase하는 방법은 다음과 같다.  
`topic` 브랜치와 `master` 브랜치의 공통 조상으로부터 `topic` 브랜치의 마지막 commit까지 모든 commit을 diff하여 `master` 브랜치의 뒤에 diff를 적용한 commit을 붙인다.

~~~sh
git checkout topic
git rebase master
~~~

## git pull

`git pull` : `git fetch` + `git merge`

## git checkout

~~~sh
git checkout HEAD~1		# 1단계 전 commit으로 되돌리기
git checkout master		# master 브랜치로 돌아온다
git checkout 8553f2		# commit 해시의 앞 6자리를 적어주면 해당  commit으로 이동한다.
~~~

## git merge

다음 명령은 `topic` 브랜치는 그대로이고, `master` 브랜치만 `topic`과 merge되고 `master` 브랜치는 merge된 결과의 최신 commit을 가리킨다.

```sh
git checkout master
git merge topic
```

## git branch

```sh
git branch		# local 브랜치
git branch -r	# remote 브랜치
git branch -a	# local & remote 브랜치
```

## git fetch

fetching은 local branch에는 영향을 주지 않는다. fetch된 commit은 remote branch의 뒤에 붙는다.  
만약 remote branch의 commit이 마음에 든다면 local branch와 merge하면 된다.

```sh
git fetch <remote>	# 모든 branch를 가져온다.
git fetch <remote> <branch>	# 특정 branch만 가져온다.
```

remote branch는 다른 사람의 commit이 담긴 branch이다.  
remote branch는 read-only 브랜치로 생각할 수 있다.

## git pull

```sh
git pull origin master
# 위 문장은 다음 문장과 같은 의미이다.
git fetch origin master
git checkout master
git merge origin/master
```

```sh
git pull <remote>		# 현재 branch의 remote copy를 가져와서 merge한다.
```

merge 대신 rebase를 하려면 다음 명령어를 사용한다.

```sh
git pull --rebase <remove>
```
## git log

commit할 때 추가한 파일/디렉터리를 같이 보여준다.

```sh
git log --name-status
```

## git remote

remote repo를 추가/제거하는 명령어는 다음과 같다.

```sh
git remote add origin git@github.com:swsnu/FAW.git
git remote remove origin
```
## git commit

다음 명령어로 commit 메시지를 수정할 수 있다. 하지만 수정 후에 push할 경우 에러가 발생하는데 이 때에는 그 아래의 명령어처럼 `--force` 옵션을 붙여서 push를 수행한다.

```sh
git commit --amend
git push --force origin master
```



