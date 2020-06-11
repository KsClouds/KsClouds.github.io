---
title: hexo
date: 2020-06-07 10:14:24
tags: [hexo, github]
cover: http://img5.imgtn.bdimg.com/it/u=43100567,1780164666&fm=26&gp=0.jpg
---
## create steps
### create repository 
create a repository in github, name it `<user-name>.github.io`
### use nodejs
- install nodejs
- `npm install -g hexo`
- `hexo init`
### change settings
- modify `_config.yml`, change `deploy.repo` to your git repo
### hexo command
- `hexo s` `hexo server`
- `hexo g` `hexo generate`
- `hexo d` `hexo deploy`
- `hexo new [scaffolds] [title]`

## upload your source
github only save your html, you can use branch to save you source.
### steps
#### new branch
create a new branch, example: `hexo`.
set it as the default branch.
#### push your code
push `scaffolds`, `source`, `themes`, `_config.yml`, `package.json` to your new branch.

## problems
Hexo启动页面显示extends includes/layout.pug block content include includes/recent-posts.pug include