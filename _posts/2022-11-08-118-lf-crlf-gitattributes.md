---
layout: post
title: 'lf와 crlf 그리고 .gitattributes'
author: 'Nostrss'
comments: true
tags: git gitattributes lf crlf
excerpt_separator:
sticky:
hidden:
---

### 윈도우에서 작성한 코드가 맥에서는 오류가 난다?

먼저 알아야 할 개념이 있다. 과거 타자기를 쓸 때 부터 내려운 개념이라고 한다.

> CR : Carriage-Return, \r

- 현재 커서를 줄 올림 없이 가장 앞으로 옮기는 동작

> LF : Line Feed, \n

- 커서는 그 자리에 둔 상황에서 종이만 한 줄 올려 줄을 바꾸는 동작

윈도우는 `CRLF` 방식, 유닉스/리눅스는 `LF`방식으로 `개행문자`(줄바꿈문자)를 처리한다.

그래서 서로 다른 운영체제(윈도우와 맥)를 쓰는 사람과 작업을 하다보면 형상관리를 이용할 때 충돌이 날 수 있다.

예를 들면 아무것도 하지 않았는데 형상관리에서 개행문자를 변경된 것으로 인식하는 경우가 생길 수도 있다.

그래서 이런 경우 주로 유닉스 방식인 `LF`로 바꾸어 형상관리(git)를 해야 한다.

### .gitattributes 파일 만들기

사용하는 IDE에서 설정하는 방법도 있겠지만 소스코드에 `.gitattributes` 파일을 생성해서 관리하는 방법이 있다.

gitignore처럼 root경로에 파일을 생성해 두기만 하면 git에 커밋하고 풀을 받거나 할 때 CRLF와 LF 신경쓰지 않고 작업을 할 수 있다.

파일은 직접 만들수도 있고 생성해주는 사이트에서 받아서 사용해도 된다.

> https://gitattributes.io/

나는 React 소스이니깐 Web Project를 선택해서 Generate 했다.

> https://gitattributes.io/api/web

```
## GITATTRIBUTES FOR WEB PROJECTS
#
# These settings are for any web project.
#
# Details per file setting:
#   text    These files should be normalized (i.e. convert CRLF to LF).
#   binary  These files are binary and should be left untouched.
#
# Note that binary is a macro for -text -diff.
######################################################################

# Auto detect
##   Handle line endings automatically for files detected as
##   text and leave all files detected as binary untouched.
##   This will handle all files NOT defined below.
*                 text=auto

# Source code
*.bash            text eol=lf
*.bat             text eol=crlf
*.cmd             text eol=crlf
*.coffee          text
*.css             text
*.htm             text diff=html
*.html            text diff=html
*.inc             text
*.ini             text
*.js              text
*.json            text
*.jsx             text
*.less            text
*.ls              text
*.map             text -diff
*.od              text
*.onlydata        text
*.php             text diff=php
*.pl              text
*.ps1             text eol=crlf
*.py              text diff=python
*.rb              text diff=ruby
*.sass            text
*.scm             text
*.scss            text diff=css
*.sh              text eol=lf
*.sql             text
*.styl            text
*.tag             text
*.ts              text
*.tsx             text
*.xml             text
*.xhtml           text diff=html

# Docker
Dockerfile        text

# Documentation
*.ipynb           text
*.markdown        text
*.md              text
*.mdwn            text
*.mdown           text
*.mkd             text
*.mkdn            text
*.mdtxt           text
*.mdtext          text
*.txt             text
AUTHORS           text
CHANGELOG         text
CHANGES           text
CONTRIBUTING      text
COPYING           text
copyright         text
*COPYRIGHT*       text
INSTALL           text
license           text
LICENSE           text
NEWS              text
readme            text
*README*          text
TODO              text

# Templates
*.dot             text
*.ejs             text
*.haml            text
*.handlebars      text
*.hbs             text
*.hbt             text
*.jade            text
*.latte           text
*.mustache        text
*.njk             text
*.phtml           text
*.tmpl            text
*.tpl             text
*.twig            text
*.vue             text

# Configs
*.cnf             text
*.conf            text
*.config          text
.editorconfig     text
.env              text
.gitattributes    text
.gitconfig        text
.htaccess         text
*.lock            text -diff
package-lock.json text -diff
*.toml            text
*.yaml            text
*.yml             text
browserslist      text
Makefile          text
makefile          text

# Heroku
Procfile          text

# Graphics
*.ai              binary
*.bmp             binary
*.eps             binary
*.gif             binary
*.gifv            binary
*.ico             binary
*.jng             binary
*.jp2             binary
*.jpg             binary
*.jpeg            binary
*.jpx             binary
*.jxr             binary
*.pdf             binary
*.png             binary
*.psb             binary
*.psd             binary
# SVG treated as an asset (binary) by default.
*.svg             text
# If you want to treat it as binary,
# use the following line instead.
# *.svg           binary
*.svgz            binary
*.tif             binary
*.tiff            binary
*.wbmp            binary
*.webp            binary

# Audio
*.kar             binary
*.m4a             binary
*.mid             binary
*.midi            binary
*.mp3             binary
*.ogg             binary
*.ra              binary

# Video
*.3gpp            binary
*.3gp             binary
*.as              binary
*.asf             binary
*.asx             binary
*.fla             binary
*.flv             binary
*.m4v             binary
*.mng             binary
*.mov             binary
*.mp4             binary
*.mpeg            binary
*.mpg             binary
*.ogv             binary
*.swc             binary
*.swf             binary
*.webm            binary

# Archives
*.7z              binary
*.gz              binary
*.jar             binary
*.rar             binary
*.tar             binary
*.zip             binary

# Fonts
*.ttf             binary
*.eot             binary
*.otf             binary
*.woff            binary
*.woff2           binary

# Executables
*.exe             binary
*.pyc             binary

# RC files (like .babelrc or .eslintrc)
*.*rc             text

# Ignore files (like .npmignore or .gitignore)
*.*ignore         text
```

혹시 `gitattributes`를 적용하지 않고 이미 올린 소스코드가 있다면?

상관 없다.

gitattributes를 적용한 후 푸쉬를 하고 기존 로컬 소스 삭제 한 다음 다시 클론을 받으면 된다.
