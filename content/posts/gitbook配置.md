---
title: Gitbook配置
date: 2022-10-09T21:40:51+08:00
lastmod: 2022-10-09T21:40:51+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - category1
tags:
  - tag1
  - tag2
# nolastmod: true
draft: true
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# gitbook 配置
```bash
# gitbook 安装流程

mkdir -p ~/.nvm/versions/node
tar xvf node-v12.22.12-linux-x64.tar.xz
mv node-v12.22.12-linux-x64 ~/.nvm/versions/node/v12.22.12

npm config set registry https://registry.npmmirror.com

npm install -g gitbook-cli

gitbook init
gitbook build
gitbook install
```

*book.json* 
```json
{
	"title": "前端家族集锦",
	"description": "重学前端，梳理自己的前端格局",
	"author": "贰拾壹先生",
	"language": "zh-hans",
	"link": {
		"sidebar": {
			"HOME": "https://www.baidu.com"
		}
	},
	"plugins": [
		"-sharing",
		"-lunr",
		"-search",
		"search-pro",
		"back-to-top-button",
		"chapter-fold",
		"expandable-chapters-small",
		"code",
		"copy-code-button",
		"advanced-emoji",
		"splitter",
		"tbfed-pagefooter",
		"ancre-navigation",
		"anchor-navigation-ex",
		"pageview-count",
		"hide-element",
		"popup",
		"anchors",
		"expandable-chapters",
		"chapter-fold",
		"page-treeview",
		"back-to-top-button",
		"page-toc-button",
		"anchor-navigation-ex",
		"ancre-navigation",
		"favicon",
		"alerts",
		"flexible-alerts",
		"todo",
		"emphasize"
	],
	"pluginsConfig": {
		"code": {
			"copyButtons": true
		},
		"github": {
			"url": "https://github.com/zhengliming"
		},
		"tbfed-pagefooter": {
			"copyright": "Copyright &copy jsbbmm.com 2021",
			"modify_label": "该文件修订时间：",
			"modify_format": "YYYY-MM-DD HH:mm:ss"
		},
		"hide-element": {
			"elements": [
				".gitbook-link",
				".copyright"
			]
		},
		"anchor-navigation-ex": {
			"showLevel": false,
			"showGoTop": false
		},
		"page-toc-button": {
			"maxTocDepth": 2,
			"minTocSize": 1
		},
		"favicon":{
			"shortcut":"_book/gitbook/images/favicon.ico",
			"bookmark":"_book/gitbook/images/favicon.ico"
		},
		"flexible-alerts": {
			"note": {
				"label": {
					"de": "Hinweis",
					"en": "Note"
				}
			},
			"tip": {
				"label": {
					"de": "Tipp",
					"en": "Tip"
				}
			},
			"warning": {
				"label": {
					"de": "Warnung",
					"en": "Warning"
				}
			},
			"danger": {
				"label": {
					"de": "Achtung",
					"en": "Attention"
				}
			}
		}
	}
}
```

## ps
```plain
移植gitbook时，除了module下的文件夹，还有一个在～/.gitbook
```