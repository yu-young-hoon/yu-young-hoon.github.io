---
layout: default
title: mac zsh 설정
parent: shell
nav_order: 206101
---

# zsh 설치
brew install zsh

## omz 설치
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# 터미널 하이라이팅, 자동완성 플러그인 설치
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# 플러그인 설정
vim ~/.zshrc

# 이부분을 찾아서 바꾸면 된다
plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
)

# oh-my-zsh 업데이트를 항상 y로 하고 싶다면 아래 추가
DISABLE_UPDATE_PROMPT=true

# oh-my-zsh 업데이트를 비활성 하고 싶다면 아래 추가
DISABLE_AUTO_UPDATE=true
