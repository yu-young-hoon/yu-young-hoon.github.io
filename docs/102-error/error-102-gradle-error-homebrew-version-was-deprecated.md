---
layout: default
title: gradle 에러 homebrew/versions was deprecated. This tap is now empty as all its formulae were migrated.
parent: error
nav_order: 102102
---

brew tab은 deprecated되고 core에 migration 되었기 때문에 아래와 같이 버전을 찾아서 직접 설치하는 방법이 있다.

```
git clone https://github.com/Homebrew/homebrew-core.git

git log master -- Formula/gradle.rb

brew unlink gradle

brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/a138a8c76dfed75f5c63117e29d95e502daef3b9/Formula/gradle.rb

/usr/local/Cellar/gradle/4.7 (199 files, 80.5MB) *
  Built from source on 2020-01-28 at 11:26:45
/usr/local/Cellar/gradle/5.2.1 (13,358 files, 235.3MB)
  Built from source on 2019-03-18 at 12:51:0
```
설치후 brew info gradle을 해보면 아래처럼 다른 버전이 설치되고

```
brew switch gradle 5.2.1
```
다시 버전을 변경할수 있다.