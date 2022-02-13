---
title: Madome API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

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

# Auth

## Create Authcode

```shell
curl \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{ "email": "user@madome.app" }' \
    "/auth/code"
```

> Body Parameters

```jsonc
{ "email": "user@madome.app" }
```

`Authcode`를 생성하고, 생성된 `Authcode`를 주어진 이메일에 전송합니다.

### HTTP Request

`POST /auth/code`

### Body Parameters

Parameter | Description
--------- | ----------
email     | 생성된 `Authcode`를 수신할 이메일 주소

### HTTP Response

Code | Description
---- | ----------
201  | `Authcode`를 생성했고 메일도 전송했어요.
404  | 주어진 이메일은 존재하지 않는 사용자의 이메일이에요.
429  | `Authcode`를 너무 많이 생성했어요.

## Create Token Pair

```shell
curl \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{ "email": "user@madome.app", "code": "vrKwuatEgq-V" }' \
    "/auth/token"
```

> Body Parameters

```jsonc
{ "email": "user@madome.app"
, "code": "vrKwuatEgq-V" }
```

> Returns Set-Cookie to HTTP Headers

```text
Set-Cookie: madome_access_token=ACCESS_TOKEN; \
            Domain=madome.app; \
            Max-Age=604800; \
            Path=/; \
            Secure; \
            HttpOnly;
Set-Cookie: madome_refresh_token=REFRESH_TOKEN; \
            Domain=madome.app; \
            Max-Age=604800; \
            Path=/; \
            Secure; \
            HttpOnly;
```

[Create Authcode](#create-authcode)에서 발신한 `Authcode`를 사용해서 `Token Pair`를 생성해요.

### HTTP Request

`POST /auth/token`

### Body Parameters

Parameter | Description |
--------- | ----------- |
email     | `Authcode`를 전달 받은 이메일 주소 |
code      | `Authcode` |

### HTTP Response

Code | Description |
---- | ----------- |
201  | `Token Pair`가 생성됐어요. |
404  | `Authcode`가 만료되었거나 존재하지 않는 사용자예요. |

## Check Access Token

```shell
curl \
    -X GET \
    "/auth/token
```

> Returns JSON

```jsonc
{ "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0" }
```

인증

### HTTP Request

`GET /auth/token`

### Query Parameters

Parameter | Description | Required |
--------- | ----------- | -------- |
role | 인증에 필요한 최소 권한. `현재는 0 ~ 1 까지만 있음` | X |

### HTTP Response

Code | Description |
---- | ----------- |
200  | 인증 성공했어요. |
401  | `Access Token`이 유효하지 않아요. |
403  | 권한이 부족해요. |

<!-- ## Check and Refresh Token Pair -->

# User

## Get Me

```shell
curl -X GET \
    "/users/@me"
```

> Returns JSON

```json
{ "id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0"
, "name": "madome"
, "email": "user@madome.app"
, "role": 0
, "created_at": "2022-01-24T08:06:25.673860Z"
, "updated_at": "2022-01-24T08:06:25.673860Z" }
```

자신의 정보를 가져와요.

### HTTP Request

`GET /users/@me`

### HTTP Response

Code | Description |
---- | ----------- |
200  | 자신의 정보를 가져오는데 성공했어요. |
404  | 인증 어케 통과했노? |

## Create User

```shell
curl \
    -X POST \
    -H "Content-Type: application/json" \
    -d '{ "name": "madome", "email": "user@madome.app", "role": 0 }' \
    "/users"
```

> Body Parameters

```jsonc
{ "name": "madome"
, "email": "user@madome.app"
, "role": 0 } // default
```

사용자를 생성해요.

### HTTP Request

`GET http://example.com/kittens/<ID>`

### Body Parameters

Parameter | Description                         | Required |
--------- | ----------------------------------- | -------- |
name      | 사용자의 이름. 서버에서 유일해야해요. 이름의 길이는 `1 ~ 20` 이에요 | O
email     | 사용자의 메일주소. 서버에서 유일해야해요. 이메일이어야 해요| O
role      | 사용자의 권한. 현재는 `0 ~ 1` 까지만 존재해요. | X

### HTTP Response

Code | Description |
---- | ----------- |
201  | 사용자를 생성했어요. |
400  | 잘못된 요청이에요. 다시 한번 확인해줄래요? |
409  | 이미 존재하는 사용자예요. |

## Delete a Specific Kitten

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

