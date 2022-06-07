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
{
    "email": "user@madome.app"
}
```

> Returns Nothing

`Authcode`를 생성하고, 생성된 `Authcode`를 주어진 이메일에 전송해요.

<aside class="notice">
토큰 미포함
</aside>

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
{
    "email": "user@madome.app",
    "code": "vrKwuatEgq-V"
}
```

> Returns Set-Cookie to HTTP Headers

```text
Set-Cookie: madome_access_token=ACCESS_TOKEN;
            Domain=madome.app;
            Max-Age=604800;
            Path=/;
            Secure;
            HttpOnly;
Set-Cookie: madome_refresh_token=REFRESH_TOKEN;
            Domain=madome.app;
            Max-Age=604800;
            Path=/;
            Secure;
            HttpOnly;
```

[Create Authcode](#create-authcode)에서 발신한 `Authcode`를 사용해서 `Token Pair`를 생성해요.

<aside class="notice">
토큰 미포함
</aside>

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
{
    "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0"
}
```

인증

### HTTP Request

`GET /auth/token`

### Query Parameters

Parameter | Description | Value | Default |
--------- | ----------- | ----- | ------- |
role | 인증에 필요한 최소 권한 | `0 ~ 1` | `0` |

### HTTP Response

Code | Description |
---- | ----------- |
200  | 인증 성공했어요. |
401  | `Access Token`이 유효하지 않아요. |
403  | 권한이 부족해요. |

## Refresh Token Pair

```shell
curl \
    -X PATCH \
    "/auth/token
```

> Returns Set-Cookie to HTTP Headers

```text
Set-Cookie: madome_access_token=ACCESS_TOKEN;
            Domain=madome.app;
            Max-Age=604800;
            Path=/;
            Secure;
            HttpOnly;
Set-Cookie: madome_refresh_token=REFRESH_TOKEN;
            Domain=madome.app;
            Max-Age=604800;
            Path=/;
            Secure;
            HttpOnly;
```

> Returns JSON

```jsonc
{
    "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0"
}
```

### HTTP Request

`PATCH /auth/token`

### HTTP Response

Code | Description |
---- | ----------- |
200  | 인증 성공했어요. |
401  | 토큰이 유효하지 않아요. |
403  | 권한이 부족해요. |

## Delete Token Pair

```shell
curl \
    -X DELETE \
    /auth/token
```

> Returns Nothing

### HTTP Request

`DELETE /auth/token`

### HTTP Response

Code | Description
---- | ---------
204 | 성공함
