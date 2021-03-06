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


## git checkout

~~~sh
git checkout HEAD~1		# 1단계 전 commit으로 되돌리기
git checkout master		# master 브랜치로 돌아온다
git checkout 8553f2		# commit 해시의 앞 6자리를 적어주면 해당  commit으로 이동한다.
~~~

또한 `git checkout`를 통해 특정 파일을 이전 commit 상태로 되돌릴 수 있다.

```sh
git checkout -- main.c
```

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

브랜치를 삭제하려면 `-d` 또는 `-D` 옵션을 사용한다.

```sh
$ git branch -d <branch>
$ git branch -D <branch>		# <branch>가 merge되지 않은 경우 -d 옵션으로는 삭제할 수 없다. 이 때 -D 사용
```

브랜치 이름을 변경하려면 `-m` 옵션을 사용한다.

```sh
$ git branch -m <old-branch> <new-branch>
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

`git pull` : `git fetch` + `git merge`

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

## git rm

파일은 삭제하지 않고 추적만 중지하고 싶다면 `--cached` 옵션을 붙인다. 만약 파일까지 삭제하려면 옵션을 빼고 실행한다.

```sh
git rm --cached .DS_Store
```

## git push

remote와 branch를 기억하려면 `-u` 옵션을 사용한다.

```sh
git push -u origin master
```

```sh
$ git config --global push.default simple	# 현재 브랜치만 push
$ git config --global push.default matching	# 로컬의 브랜치 중 remote와 일치하는 모든 브랜치 push
```

