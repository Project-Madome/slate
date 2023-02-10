# Like

## Get Likes | Dislikes

```shell
curl \
    -X GET \
    "/users/@me/likes?per-page=2" # "/users/@me/dislikes?per-page=2"
```

> Returns JSON

```jsonc
[
    {
        "kind": "book",
        "book_id": 423144,
        "is_dislike": false,
        "created_at": "2022-02-11T11:53:57.496082Z",
        "book": Book
    },
    {
        "kind": "book_tag",
        "tag_kind": "female",
        "tag_name": "loli",
        "is_dislike": false,
        "created_at": "2022-02-11T11:53:50.429997Z",
        "books": [Book, Book, Book]
    }
]
```

사용자가 좋아요한 것들을 가져와요.

### HTTP Request

`GET /users/@me/likes`

`GET /users/@me/dislikes`

### Query Parameters

Parameter | Description | Value | Default |
--------- | ----------- | ----- | ------- |
per-page | 가져올 개수 | `1 ~ 100` | `25` |
page | 페이지 | `1 ~` | `1` |
sort-by | 정렬 방법 | `created-at-desc`, `created-at-asc`, `random` | `created-at-desc` |
kind | `Like`의 종류 | `book`, `book_tag` | `null` |
books-per-page | `kind`가 `book_tag`인 경우에 포함되는 `books`의 `per-page` | `1 ~ 100` | `3`
books-page | `kind`가 `book_tag`인 경우에 포함되는 `books`의 `page` | `1 ~` | `1`
books-sort-by | `kind`가 `book_tag`인 경우에 포함되는 `books`의 `sort-by` | `id-desc`, `id-asc`, `random` | `id-desc`


### HTTP Response

Code | Description |
---- | ----------- |
200  | 성공했어요. |

## Create or Update Like | Dislike

> If book

```shell
curl \
    -X POST \
    -d '{ "kind": "book", "book_id": 123456 }' \
    "/users/@me/likes" # "/users/@me/dislikes"
```

> If book_tag

```shell
curl \
    -X POST \
    -d '{ "kind": "book_tag", "tag_kind": "female", "tag_name": "loli" }' \
    "/users/@me/likes" # "/users/@me/dislikes"
```

> Returns Nothing

`uri path`로 `is_dislike`을 구분해요.

`is_dislike`이 변경되는 경우에만 업데이트 처리가 돼요. (전에 `like`이었다면, `dislike`으로 업데이트 하기 위해서는 `/users/@me/dislikes`로 요청을 넣어야함)

### HTTP Request

`POST /users/@me/likes`

`POST /users/@me/dislikes`

### Body Parameters

#### Book

Parameter | Description | Value |
--------- | ----------- | ----- |
kind | `Like`의 종류 | `book` |
book_id | 책 ID | `0 ~` |

#### Book Tag

Parameter | Description | Value |
--------- | ----------- | ----- |
kind | `Like`의 종류 | `book_tag` |
tag_kind | 태그의 종류 | `string` |
tag_name | 태그의 이름 | `string` |

### HTTP Response

Code | Description
---- | ----------
201  | 성공했어요.
404  | 없는 작품 또는 태그예요.
409  | 이미 있는 작품 또는 태그인데, 서버에 존재하는 데이터와 `is_dislike`이 동일해서 업데이트 할 게 없어요.

## Delete Like | Dislike

> If book

```shell
curl \
    -X DELETE \
    -d '{ "kind": "book", "book_id": 123456 }' \
    "/users/@me/likes" # "/users/@me/dislikes"
```

> If book_tag

```shell
curl \
    -X DELETE \
    -d '{ "kind": "book", "tag_kind": "female", "tag_name": "loli" }' \
    "/users/@me/likes" # "/users/@me/dislikes"
```

> Returns Nothing

### HTTP Request

`DELETE /users/@me/likes`

`DELETE /users/@me/dislikes`

### Body Parameters

#### Book

Parameter | Description | Value |
--------- | ----------- | ----- |
kind | `Like`의 종류 | `book` |
book_id | 책 ID | `0 ~` |

#### Book Tag

Parameter | Description | Value |
--------- | ----------- | ----- |
kind | `Like`의 종류 | `book_tag` |
tag_kind | 태그의 종류 | `string` |
tag_name | 태그의 이름 | `string` |

### HTTP Response

Code | Description
---- | ----------
204  | 성공했어요.
404  | 없어요.
