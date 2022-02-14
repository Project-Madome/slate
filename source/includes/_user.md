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
