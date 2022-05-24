# User

## Get Me

```shell
curl -X GET \
    "/users/@me"
```

> Returns JSON

```json
{
    "id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
    "name": "madome",
    "email": "user@madome.app",
    "role": 0,
    "created_at": "2022-01-24T08:06:25.673860Z",
    "updated_at": "2022-01-24T08:06:25.673860Z"
}
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
{
    "name": "madome",
    "email": "user@madome.app",
    "role": 0 // default
}
```

> Returns Nothing

사용자를 생성해요.

### HTTP Request

`POST /users`

### Body Parameters

Parameter | Description  | Value| Required |
--------- | ------------ | ---- | -------- |
name      | 사용자의 이름 | 길이 `1 ~ 20` | O
email     | 사용자의 메일주소 | 이메일 | O
role      | 사용자의 권한 | `0 ~ 1` | X

### HTTP Response

Code | Description |
---- | ----------- |
201  | 사용자를 생성했어요. |
409  | 이미 존재하는 사용자예요. |

## Create or Update Fcm Token

```shell
curl \
    -X POST \
    -d '{ "udid": "b99a9fc0-568c-4b85-bec2-1271ed6f8bd7", "fcm_token": "YOUR_FCM_REGISTRATION_TOKEN" }' \
    "/users/@me/fcm-token"
```

> Returns Nothing

### HTTP Request

`POST /users/@me/fcm-token`

### Body Parameters

Parameter | Description | Value |
--------- | ----------- | ----- |
udid | 기기의 고유 식별자 | `uuid` |
fcm_token | firebase cloud messaging 토큰 |  |

### HTTP Response

Code | Description |
---- | ----------- |
201 | 생성 또는 갱신에 성공함 |
