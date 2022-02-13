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

아래 이미지는 서버에서 자동으로 이루어지는 `Check and Refresh Token`에 대한 순서도예요.

클라이언트에서는 토큰 관리에 대해서는 신경쓰지 않아도 돼요.

![auth-flowchart](auth-flowchart.svg)
