```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-k3u4a6@email.com",
    "username": "author-k3u4a6",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-k3u4a6@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1rM3U0YTYiLCJpYXQiOjE1OTA2MjI4OTUsImV4cCI6MTU5MDc5NTY5NX0.IMW2wt7hwZ-QUmZMKJ8NGx6AjpCMS8tZWR7TztSRwqM",
    "username": "author-k3u4a6",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-z5o4pg@email.com",
    "username": "authoress-z5o4pg",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-z5o4pg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy16NW80cGciLCJpYXQiOjE1OTA2MjI4OTUsImV4cCI6MTU5MDc5NTY5NX0.uED0tuZBuQBqjgnqvvQ5i0VIQsVN4x3watzmZOMeznE",
    "username": "authoress-z5o4pg",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-kfsc3m@email.com",
    "username": "non-author-kfsc3m",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-kfsc3m@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3Ita2ZzYzNtIiwiaWF0IjoxNTkwNjIyODk2LCJleHAiOjE1OTA3OTU2OTZ9.6pLLKe3VfAU1BXbUXeS-ohBZWvuxZ4TKCknsff-jvXQ",
    "username": "non-author-kfsc3m",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uqdlq9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622896075,
    "updatedAt": 1590622896075,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wydi2t",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622896141,
    "updatedAt": 1590622896141,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-uqdlq9
```
```
200 OK

{
  "article": {
    "createdAt": 1590622896075,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-uqdlq9",
    "updatedAt": 1590622896075,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-wydi2t
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1590622896141,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-wydi2t",
    "updatedAt": 1590622896141,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/2dgxfb
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [2dgxfb]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-wydi2t

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1590622896141,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-wydi2t",
    "updatedAt": 1590622896141,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-wydi2t

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1590622896141,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-wydi2t",
    "updatedAt": 1590622896141,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-wydi2t

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1590622896141,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-wydi2t",
    "updatedAt": 1590622896141,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-wydi2t

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-wydi2t

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-wydi2t

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-wydi2t

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-wydi2t]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-wydi2t

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-k3u4a6]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-uqdlq9/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1590622896075,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-uqdlq9",
    "updatedAt": 1590622896075,
    "favoritedBy": [
      "non-author-kfsc3m"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-uqdlq9
```
```
200 OK

{
  "article": {
    "createdAt": 1590622896075,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-uqdlq9",
    "updatedAt": 1590622896075,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-uqdlq9/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-uqdlq9_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-uqdlq9_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-uqdlq9/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1590622896075,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-uqdlq9",
    "updatedAt": 1590622896075,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-uqdlq9
```
```
200 OK

{}
```
```
GET /articles/title-uqdlq9
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-uqdlq9]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-wydi2t
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-k3u4a6]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "y2grla",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-r3j6ak",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897526,
    "updatedAt": 1590622897526,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "y2grla",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "isjzl4",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-6mx6ei",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897573,
    "updatedAt": 1590622897573,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "isjzl4",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7r3qmh",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sbelrr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897625,
    "updatedAt": 1590622897625,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7r3qmh",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "34h4c5",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-g4zxa3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897670,
    "updatedAt": 1590622897670,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "34h4c5",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "yyjxfl",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-6frhzi",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897722,
    "updatedAt": 1590622897722,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "yyjxfl",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ws417j",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ge45jw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897770,
    "updatedAt": 1590622897770,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ws417j",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "h8vifn",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-j1md28",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897827,
    "updatedAt": 1590622897827,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "h8vifn",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ufz1vi",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-27p1v2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897872,
    "updatedAt": 1590622897872,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ufz1vi",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4tcgoo",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ui6bcl",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897921,
    "updatedAt": 1590622897921,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4tcgoo",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "oe01o1",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2h8ik8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622897968,
    "updatedAt": 1590622897968,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "oe01o1",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "v544fg",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-t68vt9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898022,
    "updatedAt": 1590622898022,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "v544fg",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nq5c3o",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dga4zc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898066,
    "updatedAt": 1590622898066,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nq5c3o",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "i1vvci",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-m957n5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898128,
    "updatedAt": 1590622898128,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "i1vvci",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "l4ezvd",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-venodi",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898172,
    "updatedAt": 1590622898172,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "l4ezvd",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4dknjc",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dyz9o",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898213,
    "updatedAt": 1590622898213,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4dknjc",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lp4eej",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-yw54ey",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898247,
    "updatedAt": 1590622898247,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lp4eej",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "gno7cj",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ibip74",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898297,
    "updatedAt": 1590622898297,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "gno7cj",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "oab18y",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p56uif",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898341,
    "updatedAt": 1590622898341,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "oab18y",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qkldcy",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-1rj3oh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898376,
    "updatedAt": 1590622898376,
    "author": {
      "username": "authoress-z5o4pg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qkldcy",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7unisk",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-cjrk9b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622898448,
    "updatedAt": 1590622898448,
    "author": {
      "username": "author-k3u4a6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7unisk",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7unisk",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898448,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cjrk9b",
      "updatedAt": 1590622898448,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qkldcy",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898376,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1rj3oh",
      "updatedAt": 1590622898376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oab18y",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898341,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p56uif",
      "updatedAt": 1590622898341,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gno7cj",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898297,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ibip74",
      "updatedAt": 1590622898297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lp4eej",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898247,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yw54ey",
      "updatedAt": 1590622898247,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dknjc",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898213,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyz9o",
      "updatedAt": 1590622898213,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l4ezvd",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898172,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-venodi",
      "updatedAt": 1590622898172,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i1vvci",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898128,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m957n5",
      "updatedAt": 1590622898128,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nq5c3o",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898066,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dga4zc",
      "updatedAt": 1590622898066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v544fg"
      ],
      "createdAt": 1590622898022,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t68vt9",
      "updatedAt": 1590622898022,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oe01o1",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897968,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2h8ik8",
      "updatedAt": 1590622897968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4tcgoo",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897921,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ui6bcl",
      "updatedAt": 1590622897921,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "ufz1vi"
      ],
      "createdAt": 1590622897872,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-27p1v2",
      "updatedAt": 1590622897872,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h8vifn",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897827,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j1md28",
      "updatedAt": 1590622897827,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "ws417j"
      ],
      "createdAt": 1590622897770,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ge45jw",
      "updatedAt": 1590622897770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yyjxfl"
      ],
      "createdAt": 1590622897722,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6frhzi",
      "updatedAt": 1590622897722,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "34h4c5",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897670,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4zxa3",
      "updatedAt": 1590622897670,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7r3qmh",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897625,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sbelrr",
      "updatedAt": 1590622897625,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "isjzl4",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622897573,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6mx6ei",
      "updatedAt": 1590622897573,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y2grla"
      ],
      "createdAt": 1590622897526,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r3j6ak",
      "updatedAt": 1590622897526,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "ufz1vi"
      ],
      "createdAt": 1590622897872,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-27p1v2",
      "updatedAt": 1590622897872,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "oab18y",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898341,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p56uif",
      "updatedAt": 1590622898341,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dknjc",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898213,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyz9o",
      "updatedAt": 1590622898213,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nq5c3o",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898066,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dga4zc",
      "updatedAt": 1590622898066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4tcgoo",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897921,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ui6bcl",
      "updatedAt": 1590622897921,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "ws417j"
      ],
      "createdAt": 1590622897770,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ge45jw",
      "updatedAt": 1590622897770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7r3qmh",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897625,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sbelrr",
      "updatedAt": 1590622897625,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-z5o4pg
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qkldcy",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898376,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1rj3oh",
      "updatedAt": 1590622898376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gno7cj",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898297,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ibip74",
      "updatedAt": 1590622898297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dknjc",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898213,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyz9o",
      "updatedAt": 1590622898213,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i1vvci",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898128,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m957n5",
      "updatedAt": 1590622898128,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v544fg"
      ],
      "createdAt": 1590622898022,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t68vt9",
      "updatedAt": 1590622898022,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4tcgoo",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897921,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ui6bcl",
      "updatedAt": 1590622897921,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h8vifn",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897827,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j1md28",
      "updatedAt": 1590622897827,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yyjxfl"
      ],
      "createdAt": 1590622897722,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6frhzi",
      "updatedAt": 1590622897722,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7r3qmh",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897625,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sbelrr",
      "updatedAt": 1590622897625,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y2grla"
      ],
      "createdAt": 1590622897526,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r3j6ak",
      "updatedAt": 1590622897526,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-kfsc3m
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-k3u4a6&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7unisk",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898448,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cjrk9b",
      "updatedAt": 1590622898448,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oab18y",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898341,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p56uif",
      "updatedAt": 1590622898341,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-k3u4a6&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "lp4eej",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898247,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yw54ey",
      "updatedAt": 1590622898247,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l4ezvd",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898172,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-venodi",
      "updatedAt": 1590622898172,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7unisk",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898448,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cjrk9b",
      "updatedAt": 1590622898448,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qkldcy",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898376,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1rj3oh",
      "updatedAt": 1590622898376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oab18y",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898341,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p56uif",
      "updatedAt": 1590622898341,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gno7cj",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898297,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ibip74",
      "updatedAt": 1590622898297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lp4eej",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898247,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yw54ey",
      "updatedAt": 1590622898247,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dknjc",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898213,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyz9o",
      "updatedAt": 1590622898213,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l4ezvd",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898172,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-venodi",
      "updatedAt": 1590622898172,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i1vvci",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898128,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m957n5",
      "updatedAt": 1590622898128,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nq5c3o",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898066,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dga4zc",
      "updatedAt": 1590622898066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v544fg"
      ],
      "createdAt": 1590622898022,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t68vt9",
      "updatedAt": 1590622898022,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oe01o1",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897968,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2h8ik8",
      "updatedAt": 1590622897968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4tcgoo",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897921,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ui6bcl",
      "updatedAt": 1590622897921,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "ufz1vi"
      ],
      "createdAt": 1590622897872,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-27p1v2",
      "updatedAt": 1590622897872,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h8vifn",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897827,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j1md28",
      "updatedAt": 1590622897827,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "ws417j"
      ],
      "createdAt": 1590622897770,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ge45jw",
      "updatedAt": 1590622897770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yyjxfl"
      ],
      "createdAt": 1590622897722,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6frhzi",
      "updatedAt": 1590622897722,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "34h4c5",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897670,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4zxa3",
      "updatedAt": 1590622897670,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7r3qmh",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897625,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sbelrr",
      "updatedAt": 1590622897625,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "isjzl4",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622897573,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6mx6ei",
      "updatedAt": 1590622897573,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y2grla"
      ],
      "createdAt": 1590622897526,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r3j6ak",
      "updatedAt": 1590622897526,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-z5o4pg/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-z5o4pg",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qkldcy",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898376,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1rj3oh",
      "updatedAt": 1590622898376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gno7cj",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898297,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ibip74",
      "updatedAt": 1590622898297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dknjc",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898213,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyz9o",
      "updatedAt": 1590622898213,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i1vvci",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898128,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m957n5",
      "updatedAt": 1590622898128,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v544fg"
      ],
      "createdAt": 1590622898022,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t68vt9",
      "updatedAt": 1590622898022,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4tcgoo",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897921,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ui6bcl",
      "updatedAt": 1590622897921,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h8vifn",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897827,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j1md28",
      "updatedAt": 1590622897827,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yyjxfl"
      ],
      "createdAt": 1590622897722,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6frhzi",
      "updatedAt": 1590622897722,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7r3qmh",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897625,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sbelrr",
      "updatedAt": 1590622897625,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y2grla"
      ],
      "createdAt": 1590622897526,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r3j6ak",
      "updatedAt": 1590622897526,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-k3u4a6/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-k3u4a6",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7unisk",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898448,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cjrk9b",
      "updatedAt": 1590622898448,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qkldcy",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898376,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1rj3oh",
      "updatedAt": 1590622898376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oab18y",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898341,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p56uif",
      "updatedAt": 1590622898341,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gno7cj",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898297,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ibip74",
      "updatedAt": 1590622898297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lp4eej",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898247,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yw54ey",
      "updatedAt": 1590622898247,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dknjc",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898213,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dyz9o",
      "updatedAt": 1590622898213,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l4ezvd",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622898172,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-venodi",
      "updatedAt": 1590622898172,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i1vvci",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622898128,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m957n5",
      "updatedAt": 1590622898128,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nq5c3o",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622898066,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dga4zc",
      "updatedAt": 1590622898066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v544fg"
      ],
      "createdAt": 1590622898022,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t68vt9",
      "updatedAt": 1590622898022,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oe01o1",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897968,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2h8ik8",
      "updatedAt": 1590622897968,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4tcgoo",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897921,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ui6bcl",
      "updatedAt": 1590622897921,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "ufz1vi"
      ],
      "createdAt": 1590622897872,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-27p1v2",
      "updatedAt": 1590622897872,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "h8vifn",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897827,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j1md28",
      "updatedAt": 1590622897827,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "ws417j"
      ],
      "createdAt": 1590622897770,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ge45jw",
      "updatedAt": 1590622897770,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yyjxfl"
      ],
      "createdAt": 1590622897722,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6frhzi",
      "updatedAt": 1590622897722,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "34h4c5",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1590622897670,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g4zxa3",
      "updatedAt": 1590622897670,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7r3qmh",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1590622897625,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sbelrr",
      "updatedAt": 1590622897625,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "isjzl4",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1590622897573,
      "author": {
        "username": "author-k3u4a6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6mx6ei",
      "updatedAt": 1590622897573,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "y2grla"
      ],
      "createdAt": 1590622897526,
      "author": {
        "username": "authoress-z5o4pg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r3j6ak",
      "updatedAt": 1590622897526,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "34h4c5",
    "tag_3",
    "tag_mod_2_1",
    "tag_mod_3_0",
    "7r3qmh",
    "tag_2",
    "tag_mod_2_0",
    "tag_mod_3_2",
    "4dknjc",
    "tag_14",
    "isjzl4",
    "tag_1",
    "tag_mod_3_1",
    "lp4eej",
    "tag_15",
    "7unisk",
    "tag_19",
    "tag_5",
    "ws417j",
    "l4ezvd",
    "tag_13",
    "qkldcy",
    "tag_18",
    "tag_7",
    "ufz1vi",
    "oe01o1",
    "tag_9",
    "i1vvci",
    "tag_12",
    "tag_4",
    "yyjxfl",
    "gno7cj",
    "tag_16",
    "tag_a",
    "tag_b",
    "4tcgoo",
    "tag_8",
    "tag_0",
    "y2grla",
    "h8vifn",
    "tag_6",
    "nq5c3o",
    "tag_11",
    "oab18y",
    "tag_17",
    "tag_10",
    "v544fg"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-q0n3ye@email.com",
    "username": "author-q0n3ye",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-q0n3ye@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1xMG4zeWUiLCJpYXQiOjE1OTA2MjI4OTksImV4cCI6MTU5MDc5NTY5OX0.VyIe1MRsvEICc10g0VRHShvnE-iUwNJcJQLmdjpY9L0",
    "username": "author-q0n3ye",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-gpc7zl@email.com",
    "username": "commenter-gpc7zl",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-gpc7zl@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1ncGM3emwiLCJpYXQiOjE1OTA2MjI4OTksImV4cCI6MTU5MDc5NTY5OX0.DNmbWjlRL1yxlMzgmDWEaV4bET2TQIBMqeEbgXXU7Gk",
    "username": "commenter-gpc7zl",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7uz5r6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1590622899978,
    "updatedAt": 1590622899978,
    "author": {
      "username": "author-q0n3ye",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment f7i4mn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "bd78337a-58de-4970-8ad0-6a4ded73448f",
    "slug": "title-7uz5r6",
    "body": "test comment f7i4mn",
    "createdAt": 1590622900009,
    "updatedAt": 1590622900009,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment vvigqv"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "d7fbced6-022d-4e63-aa73-a96c7ac00405",
    "slug": "title-7uz5r6",
    "body": "test comment vvigqv",
    "createdAt": 1590622900054,
    "updatedAt": 1590622900054,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment urufmu"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b0536e4b-083d-46b5-a71d-01f3f69ffece",
    "slug": "title-7uz5r6",
    "body": "test comment urufmu",
    "createdAt": 1590622900089,
    "updatedAt": 1590622900089,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment obpvz9"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "d48decca-de97-4d93-868a-dda67095823e",
    "slug": "title-7uz5r6",
    "body": "test comment obpvz9",
    "createdAt": 1590622900123,
    "updatedAt": 1590622900123,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment ei4wmu"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "a98f7a0a-530a-40bb-a200-a3e999e4a32d",
    "slug": "title-7uz5r6",
    "body": "test comment ei4wmu",
    "createdAt": 1590622900159,
    "updatedAt": 1590622900159,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment h281yu"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "d396b757-ff2f-4c16-8694-dc9adb6889de",
    "slug": "title-7uz5r6",
    "body": "test comment h281yu",
    "createdAt": 1590622900202,
    "updatedAt": 1590622900202,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment w2ehm9"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b2806bf5-4404-49b1-a504-b3a55ad6c45c",
    "slug": "title-7uz5r6",
    "body": "test comment w2ehm9",
    "createdAt": 1590622900244,
    "updatedAt": 1590622900244,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment w6gina"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fa5c6a04-481e-4127-9106-1104eef750fb",
    "slug": "title-7uz5r6",
    "body": "test comment w6gina",
    "createdAt": 1590622900305,
    "updatedAt": 1590622900305,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment qb9isg"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "87ae2dd0-5517-4af0-96b2-f460a780761a",
    "slug": "title-7uz5r6",
    "body": "test comment qb9isg",
    "createdAt": 1590622900361,
    "updatedAt": 1590622900361,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-7uz5r6/comments

{
  "comment": {
    "body": "test comment 2ff78y"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "8f08ce29-a079-47f4-a747-43fab1380d1c",
    "slug": "title-7uz5r6",
    "body": "test comment 2ff78y",
    "createdAt": 1590622900408,
    "updatedAt": 1590622900408,
    "author": {
      "username": "commenter-gpc7zl",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-7uz5r6/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-7uz5r6/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment uq04yq"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-7uz5r6/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1590622900305,
      "id": "fa5c6a04-481e-4127-9106-1104eef750fb",
      "body": "test comment w6gina",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900305
    },
    {
      "createdAt": 1590622900123,
      "id": "d48decca-de97-4d93-868a-dda67095823e",
      "body": "test comment obpvz9",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900123
    },
    {
      "createdAt": 1590622900054,
      "id": "d7fbced6-022d-4e63-aa73-a96c7ac00405",
      "body": "test comment vvigqv",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900054
    },
    {
      "createdAt": 1590622900244,
      "id": "b2806bf5-4404-49b1-a504-b3a55ad6c45c",
      "body": "test comment w2ehm9",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900244
    },
    {
      "createdAt": 1590622900159,
      "id": "a98f7a0a-530a-40bb-a200-a3e999e4a32d",
      "body": "test comment ei4wmu",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900159
    },
    {
      "createdAt": 1590622900202,
      "id": "d396b757-ff2f-4c16-8694-dc9adb6889de",
      "body": "test comment h281yu",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900202
    },
    {
      "createdAt": 1590622900361,
      "id": "87ae2dd0-5517-4af0-96b2-f460a780761a",
      "body": "test comment qb9isg",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900361
    },
    {
      "createdAt": 1590622900009,
      "id": "bd78337a-58de-4970-8ad0-6a4ded73448f",
      "body": "test comment f7i4mn",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900009
    },
    {
      "createdAt": 1590622900408,
      "id": "8f08ce29-a079-47f4-a747-43fab1380d1c",
      "body": "test comment 2ff78y",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900408
    },
    {
      "createdAt": 1590622900089,
      "id": "b0536e4b-083d-46b5-a71d-01f3f69ffece",
      "body": "test comment urufmu",
      "slug": "title-7uz5r6",
      "author": {
        "username": "commenter-gpc7zl",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1590622900089
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-7uz5r6/comments/bd78337a-58de-4970-8ad0-6a4ded73448f
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-7uz5r6/comments/d7fbced6-022d-4e63-aa73-a96c7ac00405
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-gpc7zl]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-7uz5r6/comments/d7fbced6-022d-4e63-aa73-a96c7ac00405
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-7uz5r6/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "username": "user1-0.93zs59tvz3r",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw",
    "username": "user1-0.93zs59tvz3r",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "username": "user1-0.93zs59tvz3r",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.93zs59tvz3r]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.93zs59tvz3r@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.93zs59tvz3r@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw",
    "username": "user1-0.93zs59tvz3r",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.960xbd9t4qj",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.960xbd9t4qj]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "password": "0.kjk28lzzfw"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.93zs59tvz3r@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw",
    "username": "user1-0.93zs59tvz3r",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.93zs59tvz3r
```
```
200 OK

{
  "profile": {
    "username": "user1-0.93zs59tvz3r",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.38zlk4sg5k3
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.38zlk4sg5k3]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.xMUHVSuC5As8O9tIqjlx9UAPk1ZegyA4adGKF6Qn3Lo",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.mypf1sajidi",
    "email": "user2-0.mypf1sajidi@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.mypf1sajidi@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAubXlwZjFzYWppZGkiLCJpYXQiOjE1OTA2MjI5MDEsImV4cCI6MTU5MDc5NTcwMX0.JS7BB6IFBCylEyl5SdzRagKmt-03Sk93L5iEDpM1dPE",
    "username": "user2-0.mypf1sajidi",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.93zs59tvz3r@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.93zs59tvz3r",
    "email": "updated-user1-0.93zs59tvz3r@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.93zs59tvz3r",
    "email": "updated-user1-0.93zs59tvz3r@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.93zs59tvz3r",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.93zs59tvz3r",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuOTN6czU5dHZ6M3IiLCJpYXQiOjE1OTA2MjI5MDAsImV4cCI6MTU5MDc5NTcwMH0.ffWPB_vtXJ11PEjEAWhWuayOcA87HCnzCV-Y0_v0eSw"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.7qmdddg06im@email.com",
    "username": "user2-0.7qmdddg06im",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.7qmdddg06im@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuN3FtZGRkZzA2aW0iLCJpYXQiOjE1OTA2MjI5MDEsImV4cCI6MTU5MDc5NTcwMX0.U2KXm2cdtsGOQplup_jSHrBy2PDaWCqYnQHrEeLbkv8",
    "username": "user2-0.7qmdddg06im",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.7qmdddg06im@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.7qmdddg06im@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-05-27T23:41:41.544Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
