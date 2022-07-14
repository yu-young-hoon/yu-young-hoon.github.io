---
layout: default
title: git 에러 error: failed to push some refs to
parent: error
nav_order: 102400
---

저장소 미러본을 만들기 위해 복제 하는 와중에 발생한 에러

* git clone --mirror https://some-site/some-repo.git
* cd ad-web.git
* git remote set-url --push origin https://some-site/some-repo.git
* git push --mirror https://some-site/some-repo-back.git
순서로 진행하였다.

![](/docs/attach/git-error-mirror01.png)
```html
! [remote rejected]     hotfix/asdf-2164 -> hotfix/asdf-2164 (pre-receive hook declined)
...
...
...
error: failed to push some refs to 'https://some-site/some-repo-back.git'
```
메시지 발생

![](/docs/attach/git-error-mirror02.png)
* 원인은 git의 레퍼런스 포인터 중 pull request가 문제였다
* git show-ref | cut -d' ' -f2 | grep 'pull-request' | xargs -L1 git update-ref -d
* 브랜치와 태그 래퍼런스는 남기고 pull request를 삭제하여 다시 진행하면 잘 작동 된다
* 참고로 mac에서 진행했기 때문에 xargs는 리눅스와 옵션이 다른것 같다

### 참고링크
* https://stackoverflow.com/questions/37985275/how-can-i-exclude-pull-requests-from-git-mirror-clone
