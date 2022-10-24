# Library

## About Tags

태그는 `[kind, name]`와 같이 tuple로 이루어져 있으며,`[female, double penetration]` 또는 `[artist, nunnu]` 와 같이 사용합니다.

<!-- URL에 사용해야 하는 경우에는 `kind-name`와 같이 사용하면 되며, `female-double-penetration` 또는 `artist-nunnu` 와 같이 사용합니다. -->

### Tag Kind

* `artist`
* `series`
* `group`
* `female`
* `male`
* `misc`

## Add Book

```shell
curl \
    -X POST \
    -d '{
            "id": 1242676,
            "title": "Soreike! Pan Koujou! - Go for it! the Bread factory! | 나가자! 빵공장!",
            "kind": "manga",
            "page": 21,
            "language": "korean",
            "tags": [
                ["artist", "nunnu"],
                ["female", "anal"],
                ["female", "bondage"],
                ["female", "machine"],
                ["female", "double penetration"],
                ["female", "sole female"],
                ["female", "tickling"],
                ["female", "schoolgirl uniform"],
            ],
            "created_at": "2022-01-31T17:12:00.000Z"
        }' \
    "/books"
```

> Returns Nothing

작품을 업로드해요.

### HTTP Request

`POST /books`

### Body Parameters

Parameter | Description | Value 
--------- | ----------- | ---- 
id | 작품 번호 | `1 ~`
title | 작품 제목 | `string`
kind | 작품 종류 | `doujinshi`, `manga`, `artist_cg`, `game_cg`
page | 작품 분량 | `1 ~`
tags | 작품 태그 | `List<Tag>`
created_at | 작품 생성 시간 | `timestamp ms`, `iso8601`, `rfc2822`

### HTTP Response

Code | Description
---- | ----------
201  | 성공했어요.
409  | 이미 있어요.


## Get Book By Id

```shell
curl \
    -X GET \
    /books/1242676
```

> Returns JSON

```jsonc
{
    "id": 1242676,
    "title": "Soreike! Pan Koujou! - Go for it! the Bread factory! | 나가자! 빵공장!",
    "kind": "manga",
    "language": "한국어",
    "page": 21,
    "tags": [
        ["artist", "nunnu"],
        ["female", "anal"],
        ["female", "bondage"],
        ["female", "double penetration"],
        ["female", "machine"],
        ["female", "schoolgirl uniform"],
        ["female", "sole female"],
        ["female", "tickling"]
    ],
    "created_at": "2018-06-23T06:07:00.000Z",
    "updated_at": "2018-06-23T06:07:00.000Z",
    "released": true
}
```

### HTTP Request

`GET /books/:book_id`

### URL Parameters

Parameter | Description | Value
--------- | ----------- | -----
book_id | 작품 번호 | `1 ~`

### HTTP Response

Code | Description
---- | ----------
200 | 가져오는데 성공함
404 | 작품이 없음

## Get Books

```shell
curl \
    -X GET \
    /books?per-page=2
```

> Returns JSON

```jsonc
[
    {
        "id": 2128614,
        "title": "Gifu to... Zenpen | 시아버님과... 전편",
        "kind": "manga",
        "language": "korean",
        "page": 30,
        "tags": [
            ["artist", "rocket monkey"],
            ["female", "anal"],
            ["female", "anal intercourse"],
            ["female", "beauty mark"],
            ["female", "milf"],
            ["male", "bald"],
            ["male", "bbm"],
            ["male", "sole male"]
        ],
        "created_at": "2022-01-31T17:12:00.000Z",
        "updated_at": "2022-01-31T17:12:00.000Z",
        "released": true
    },
    {
        "id": 2128532,
        "title": "Kura | 곳간",
        "kind": "doujinshi",
        "language": "korean",
        "page": 34,
        "tags": [
            ["series", "original"],
            ["female", "eye-covering bang"],
            ["female", "giantess"],
            ["female", "sole female"],
            ["male", "sole male"],
            ["misc", "mosaic censorship"]
        ],
        "created_at": "2022-01-31T15:59:00.000Z",
        "updated_at": "2022-01-31T15:59:00.000Z",
        "released": true
    }
]
```

### HTTP Request

`GET /books`

### Query Parameters

Parameter | Description | Value | Default
--------- | ----------- | ----- | ------
per-page | per page | `1 ~ 100` | `25`
page | page | `1 ~` | `1`
kind | 작품 종류 | `doujinshi`, `manga`, `artist-cg`, `game-cg` | `null`
sort-by | 정렬 방법 | `id-desc`, `id-asc`, `random` | `id-desc`
less-than | 주어진 id 보다 작은 작품들만 | `1 ~` | `null`
more-than | 주어진 id 보다 큰 작품들만 | `1 ~` | `null`

### HTTP Response

Code | Description
---- | ----------
200  | 가져오는데 성공함

## Get Books By Ids

```shell
curl \
    -X GET \
    /books?ids[]=1242676&ids[]=1918527
```

> Returns JSON

```jsonc
[
    {
        "id": 1242676,
        "title": "Soreike! Pan Koujou! - Go for it! the Bread factory! | 나가자! 빵공장!",
        "kind": "manga",
        "language": "한국어",
        "page": 21,
        "tags": [
            ["artist", "nunnu"],
            ["female", "anal"],
            ["female", "bondage"],
            ["female", "double penetration"],
            ["female", "machine"],
            ["female", "schoolgirl uniform"],
            ["female", "sole female"],
            ["female", "tickling"]
        ],
        "created_at": "2018-06-23T06:07:00.000Z",
        "updated_at": "2018-06-23T06:07:00.000Z",
        "released": true
    },
    {
        "id": 1918527,
        "title": "Maji Seiyoku 1000% |  정말 성욕 1000%",
        "kind": "manga",
        "language": "korean",
        "page": 24,
        "tags": [
            ["artist", "nunnu"],
            ["female", "schoolgirl uniform"],
            ["female", "sole female"],
            ["male", "teacher"]
        ],
        "created_at": "2021-05-26T07:43:00.000Z",
        "updated_at": "2021-05-26T07:43:00.000Z",
        "released": true
    }
]
```

주어진 작품 번호 중에 없는 작품은 제외하고, 주어진 순서대로 작품 정보를 드려요.

### HTTP Request

`GET /books`

### Query Parameters

Parameter | Description | Value
--------- | ----------- | -----
ids | 작품 번호들 | `List<1 ~>`

### HTTP Response

Code | Description
---- | ----------
200  | 성공함


## Get Books By Tags

```shell
curl \
    -X GET \
    # /books?tags[]=artist-nunnu&per-page=2
    # 또는
    /books?tags[0][0]=artist&tags[0][1]=nunnu&per-page=2
```

> Returns JSON

```jsonc
[
    [
        ["artist", "nunnu"],
        [
            {
                "id": 2070089,
                "title": "Jikken Shimasho!? | 실험합시다!?",
                "kind": "manga",
                "language": "korean",
                "page": 20,
                "tags": [
                    ["artist", "nunnu"],
                    ["female", "lab coat"],
                    ["female", "schoolgirl uniform"],
                    ["female", "sole female"],
                    ["male", "collar"],
                    ["male", "schoolboy uniform"],
                    ["male", "sole male"]
                ],
                "created_at": "2021-11-26T03:12:00.000Z",
                "updated_at": "2021-11-26T03:12:00.000Z",
                "released": true
            },
            {
                "id": 1995673,
                "title": "Hikkoshi zamen ikagadesuka? | 이사 정액은 어떠신가요?",
                "kind": "manga",
                "language": "korean",
                "page": 22,
                "tags": [
                    ["artist", "nunnu"],
                    ["female", "big breasts"],
                    ["female", "blowjob"],
                    ["female", "nakadashi"],
                    ["female", "sole female"],
                    ["male", "glasses"],
                    ["male", "sole male"],
                    ["male", "virginity"]
                ],
                "created_at": "2021-08-28T08:34:00.000Z",
                "updated_at": "2021-08-28T08:34:00.000Z",
                "released": true
            }
        ]
    ]
]
```

`List<((Kind, Name), List<Book>)>`

### HTTP Request

`GET /books`

### Query Parameters

Parameter | Description | Value
--------- | ----------- | ----
tags | 작품 태그들 | `List<Tag>`

### HTTP Response

Code | Description
---- | ---------
200  | 성공함

## Get Book Image List

```shell
curl \
    -X GET \
    /books/:book_id/images
```

> Returns JSON

```jsonc
[
    "1.jpg",
    "2.jpg",
    "3.jpg",
    "4.jpg",
    "5.jpg",
    "6.jpg",
    "7.jpg",
    "8.jpg",
    "9.jpg",
    "10.jpg",
    "11.jpg",
    "12.jpg",
    "13.jpg",
    "14.jpg",
    "15.jpg",
    "16.jpg",
    "17.jpg",
    "18.jpg",
    "19.jpg",
    "20.jpg",
    "21.jpg",
]
```

### HTTP Request

`GET /books/:book_id/images`

### URL Parameters

Parameter | Description | Value
--------- | ----------- | -----
book_id | 작품 번호 | `1 ~`

### HTTP Response

Code | Description
---- | ----------
200  | 성공함
404  | 작품이 없음

## Get Book Image

```shell
curl \
    -X GET \
    /books/:book_id/images/:file_name
```

> Returns Image

jpg, png, gif, webp, avif 등

file server로 redirect 해주는 방식임

### HTTP Request

`GET /books/:book_id/images/:file_name`

### URL Parameters

Parameter | Description | Value
--------- | ----------- | -----
book_id | 작품 번호 | `1 ~`
file_name | 확장자를 포함한 이미지 파일 이름 | `string`

## Release Book

```shell
curl \
    -X PATCH \
    /books/1242676/release
```

> Returns Nothing

작품 릴리즈

### HTTP Request

`PATCH /books/:book_id/release`

### URL Parameters

Parameter | Description | Value
----------|-------------|------
book_id | 작품 번호 | `1 ~`

### HTTP Response

Code | Description
---- | ----------
204  | 성공함
404  | 작품이 없음


## Search Books

```shell
curl \
    -X GET \
    /books/search?q=female%20loli%20AND%20female%20anal&per-page=2
```

> Returns JSON, Get Books와 같음

현재는 영어만 지원하는데, 한글도 지원할 예정

### About Search Query

지원하는 연산자는 `AND`, `OR`, `NOT` 이며, `female loli AND (NOT female anal)`과 같은 형식으로 사용하면 돼요

### HTTP Request

`GET /books/search`

### Query Parameters

Parameter | Description | Value | Default
--------- | ----------- | ----- | ------
q | search query | `string` | `null`
search-kind | 검색 종류 | `title`, `tag` | `null`
book-kind | 작품 종류 | `doujinshi`, `manga`, `artist-cg`, `game-cg` | `null`
per-page | per page | `1 ~ 100` | `25`
page | page | `1 ~` | `1`
sort-by | 정렬 방법 | `id-asc`, `id-desc`, `rank-asc`, `rank-desc`, `random` | `rank-desc`

### HTTP Response

Code | Description
---- | ----------
200  | 성공함


## Search Books Query Completion

```shell
curl \
    -X GET \
    /books/search/completion?q=female%20l&search-kind=tag&per-page=5
```

> Returns JSON

```jsonc
[
    {
        "keyword": "female lab coat",
        "completion": "ab coat"
    },
    {
        "keyword": "female lactation",
        "completion": "actation"
    },
    {
        "keyword": "female large insertions",
        "completion": "arge insertions"
    },
    {
        "keyword": "female large tattoo",
        "completion": "arge tattoo"
    },
    {
        "keyword": "female latex",
        "completion": "atex"
    }
]
```

검색 쿼리 자동완성

검색 결과랑은 다를 수 있어요

`completion`은 `search-kind`가 `tag`인 경우에만 제공돼요

### HTTP Request

`GET /books/search/completion`

### Query Parameters

Parameter | Description | Value | Default
--------- | ----------- | ----- | ------
q | search query | `string` | `null`
search-kind | 검색 종류 | `title`, `tag` | `null`
per-page | per page | `1 ~ 100` | `25`
page | page | `1 ~` | `1`

### HTTP Response

Code | Description
---- | ----------
200  | 성공함
