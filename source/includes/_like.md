# Like

## Get Likes

```shell
curl \
    -X GET \
    "/users/@me/likes"
```

> Returns JSON

```jsonc
[
    {
        "kind": "book",
        "book_id": 123451,
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-10T14:59:06.656643Z"
    },
    {
        "kind": "book",
        "book_id": 123452,
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-10T14:59:16.698506Z"
    },
    {
        "kind": "book_tag",
        "tag_kind": "female",
        "tag_name": "netorare",
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-10T16:20:20.060132Z"
    },
    {
        "kind": "book_tag",
        "tag_kind": "female",
        "tag_name": "rape",
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-11T11:53:43.908101Z"
    },
    {
        "kind": "book_tag",
        "tag_kind": "female",
        "tag_name": "loli",
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-11T11:53:50.429997Z"
    },
    {
        "kind": "book",
        "book_id": 42314,
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-11T11:53:55.453460Z"
    },
    {
        "kind": "book",
        "book_id": 423144,
        "user_id": "1e441e4d-f065-4f30-8c59-7e725f18ecf0",
        "created_at": "2022-02-11T11:53:57.496082Z"
    }
]
```

사용자가 좋아요한 것들을 가져와요.

### HTTP Request

`GET /users/@me/likes`

### Query Parameters

Parameter | Description | Default |
--------- | ----------- | ------- |
offset | `1 ~ 100` | `25` |
page | `1 이상` | `1` |
sort-by | `created-at-desc`, `created-at-asc`, `random` | `created-at-desc` |
kind | `book`, `book_tag` | `null` |


### HTTP Response

Code | Description |
---- | ----------- |
200  | 성공했어요. |

## Create Like

> If book

```shell
curl \
    -X POST \
    -d '{ "kind": "book", "book_id": 123456 }' \
    "/users/@me/likes"
```

> If book_tag

```shell
curl \
    -X POST \
    -d '{ "kind": "book", "tag_kind": "female", "tag_name": "loli" }' \
    "/users/@me/likes"
```

> Returns Nothing

### HTTP Request

`POST /users/@me/likes`

### Body Parameters

#### Book

Parameter | Description
--------- | ----------
kind | `book`
book_id | 책 ID

#### Book Tag

Parameter | Description
--------- | ----------
kind | `book_tag`
tag_kind | 책 태그의 종류 
tag_name | 태그의 이름

### HTTP Response

Code | Description
---- | ----------
201  | 성공했어요.
409  | 이미 있어요.

## Delete Like

> If book

```shell
curl \
    -X DELETE \
    -d '{ "kind": "book", "book_id": 123456 }' \
    "/users/@me/likes"
```

> If book_tag

```shell
curl \
    -X DELETE \
    -d '{ "kind": "book", "tag_kind": "female", "tag_name": "loli" }' \
    "/users/@me/likes"
```

> Returns Nothing

### HTTP Request

`DELETE /users/@me/likes`

### Body Parameters

#### Book

Parameter | Description
--------- | ----------
kind | `book`
book_id | 책 ID

#### Book Tag

Parameter | Description
--------- | ----------
kind | `book_tag`
tag_kind | 책 태그의 종류 
tag_name | 태그의 이름

### HTTP Response

Code | Description
---- | ----------
204  | 성공했어요.
404  | 없어요.
