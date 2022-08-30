---
layout: default
title: tool git 명령어
parent: tool
nav_order: 407111
---

==git checkout==
* git checkout -b feature/some-issue  브랜치 생성 및 이동
* git checkout -b 생성할브랜치이름 원격브랜치이름
* git checkout feature/some-issue 브랜치 이동




==git pull==
* git pull
* fetch와 merge가 병합된 형태
* rebase후 pull을 하려고 할때 conflict가 나면 git reset --hard origin/feature/AD-255처럼 reset을 강제로 해야한다




==git push==
* git push
* git push -f 강제로 푸시
* git push --force-with-lease 강제로 푸시하지만 원격 브랜치에 타인의 커밋 내역이 없을때 가능하도록 제한
* git push origin --force feature/remove-history:master 다른 브랜치에 덮기




==git merge==
git merge <branch>
<source>
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
	[--no-verify] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [-F <file>] [<commit>…​]
git merge (--continue | --abort | --quit)
</source>




==git config==
* 설정확인
  ** git config --list
* user 이름 글로벌 설정
  ** git config --global user.name "simuruk"



{| class="wikitable"
| 명령어                            || 설명
|-
| git status                      || 상태 보기
|-
| git branch                      || 브랜치 리스트 보기
|-
| git branch '브랜치 이름'           || 브랜치 생성
|-
|
|-
|
|-
| git rebase master               || 마스터 부터 시작하도록 rebase
|-
| git rebase -i HEAD~2            || 2개 커밋 리베이스
|-
| git rebase --abort              || 리베이스 취소
|-
| git push --force-with-lease     || 강제 푸시 안전
|-
| git push -f                     || 강제 푸시
|}

==참고 링크==
* [https://git-scm.com/docs git documents]
* [https://backlog.com/git-tutorial/kr/intro/intro1_1.html git intro 1]
* [https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html git intro 2]
* [https://blog.ull.im/engineering/2019/03/10/logs-on-git.html git commit message]
* [https://meetup.toast.com/posts/106?fbclid=IwAR2-0JzQY1_nra1XjTKIOScI9cHvuSNJrernv0DfXHN8Ckc1HtEOk3KqmKU git commit message2]
