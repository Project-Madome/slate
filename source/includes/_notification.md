# Notification

## Get Notifications

```shell
curl \
    -X GET \
    "/users/@me/notifications"
```

> Returns JSON

```json
[
    {
        "kind": "book",
        "book_id": 123458,
        "book_tags": [
            [
                "female",
                "anal"
            ]
        ],
        "created_at": "2022-02-14T11:32:27.485749Z"
    },
    {
        "kind": "book",
        "book_id": 123452,
        "book_tags": [
            [
                "female",
                "large insertions"
            ],
            [
                "female",
                "anal"
            ]
        ],
        "created_at": "2022-02-14T09:13:14.591283Z"
    },
    {
        "kind": "book",
        "book_id": 123456,
        "book_tags": [
            [
                "female",
                "loli"
            ],
            [
                "female",
                "rape"
            ]
        ],
        "created_at": "2022-02-14T09:13:14.591272Z"
    }
]
```

아직은 `kind`가 하나밖에 존재하지 않아요.

### HTTP Request

`GET /users/@me/notifications`

### Query Parameters

Parameter | Description | Value | Default |
--------- | ----------- | ----- | ------- |
kind | 알림의 종류 | `book` | `null` |
sort-by | 정렬 방법 | `created-at-desc`, `created-at-asc` | `created-at-desc` |
per-page | 가져올 개수 | `1 ~ 100` | `25` |
page | 페이지 | `1 ~` | `1` |

### HTTP Response

Code | Description |
---- | ----------- |
200  | 성공 |
