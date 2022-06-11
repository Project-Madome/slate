# History

## Get Histories

```shell
curl \
    -X GET \
    /users/@me/histories?per-page=2
```

> Returns JSON

```jsonc
[
    {
        "kind": "book",
        "book_id": 2217180,
        "page": 3,
        "created_at": "2022-05-19T04:02:50.691Z",
        "updated_at": "2022-05-20T05:21:44.866Z",
        "book": Book
    },
    {
        "kind": "book",
        "book_id": 1394806,
        "page": 1,
        "created_at": "2022-03-09T13:43:48.727Z",
        "updated_at": "2022-05-20T05:11:13.011Z",
        "book": Book
    }
]
```

유효하지 않는 데이터가 있는 경우(예를 들면, 없는 작품에 대한 History)에는 응답에서 해당 데이터는 제외함

### HTTP Request

`GET /users/@me/histories`

### Query Parameters

Parameter | Description | Value | Default
--------- | ----------- | ----- | ------
per-page | per page | `1 ~ 100` | `25`
page | page | `1 ~` | `1`
sort-by | 정렬 방법 | `created-at-desc`, `created-at-asc`, `updated-at-desc`, `updated-at-asc`, `random` | `updated-at-desc`

### HTTP Response

Code | Description
---- | ----------
200 | 성공함

## Create or Update History

```shell
curl \
    -X POST \
    /users/@me/histories
```

> Returns Nothing

### HTTP Request

`POST /users/@me/histories`

### Body Parameters

Parameter | Description | Value
--------- | ----------- | -----
kind | 히스토리의 종류 | `book`
book_id | 작품 번호 | `1 ~`
page | 마지막으로 본 페이지 | `1 ~`

### HTTP Response

Code | Description
---- | ----------
201 | 성공함
404 | 없는 작품이에요

## Delete History

```shell
curl \
    -X DELETE \
    /users/@me/histories
```

> Returns Nothing

### HTTP Request

### Body Parameters

Parameter | Description | Value
--------- | ----------- | ----
kind | 히스토리의 종류 | `book`
book_id | 작품 번호 | `1 ~`

### HTTP Response

Code | Description
---- | ---------
204 | 성공함
404 | 없어요
