---
layout: default
title: tool homebrew 설치 및 사용법
parent: tool
nav_order: 407117
---

==Homebrew 설치==
<source>
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
</source>

==brew 검색==
brew search java

==mysql 설치==
<source>
brew install mysql@5.7
brew services start mysql@5.7
brew link mysql@5.7 --force
mysqld --help --verbose | grep my.cnf
</source>

==nvm 설치==
<source>
brew install nvm
mkdir ~/.nvm
.profile
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
</source>

==node 설치==
<source>
nvm install v8.12.0
nvm use v8.12.0
</source>

==brew info mysql==
<source>
brew --prefix nvm
</source>
