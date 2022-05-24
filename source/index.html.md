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
  - notification
  - history
  - library

search: false

code_clipboard: true

meta:
  - name: description
    content: Documentation for Madome API
---

# Introduction

```shell
curl \
    -H "Cookie: madome_access_token=ACCESS_TOKEN; madome_refresh_token=REFRESH_TOKEN" \
    "api_endpoint_here"
```

마도메 API

요청하려는 API 설명에 토큰 미포함에 대한 설명이 있지 않으면 토큰을 포함해서 요청을 보내면 돼요.

토큰은 `HTTP Cookie`를 통해 관리되고, 토큰 인증 및 재발급은 인증이 필요한 API 엔드포인트에서 처리해요.

클라이언트는 요청을 보낼 때마다 `HTTP Cookie`에 토큰을 포함시키기만 하면 된다는 말이에요.

아래 이미지는 인증 서버에서 실행되는 `Check and Refresh Token`에 대한 순서도예요.

![auth-flowchart](auth-flowchart.svg)

# Naming rules

`Url`에 포함된 데이터들(e.g. querystring)는 `kebab-case`를 사용해요.

`Body`를 통해 오고 가는 데이터들은 `snake_case`를 사용해요.

# Querystring parser

[qs](https://www.npmjs.com/package/qs)를 사용하고 있어요.
