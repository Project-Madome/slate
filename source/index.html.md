---
title: Madome API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/Project-Madome/slate'>Documentation Powered by Slate</a>

includes:
  - errors
  - auth
  - user
  - like

search: false

code_clipboard: true

meta:
  - name: description
    content: Documentation for Madome API
---

# Introduction

```shell
curl "api_endpoint_here" \
    -H "Cookie: madome_access_token=ACCESS_TOKEN; madome_refresh_token=REFRESH_TOKEN"
```

마도메 API

요청하려는 API 설명에 토큰 미포함에 대한 설명이 있지 않으면 토큰을 포함해서 요청을 보내면 돼요.

![auth-flowchart](auth-flowchart.svg)
