#### Request with user password but two factor authentification is in the way

```
$ curl -v -u serbanghita https://api.github.com/user
```

```
GET /user HTTP/1.1
Authorization: Basic c2VyYmFuZ2hpdGF0ZXN0MTIz
User-Agent: curl/7.30.0
Host: api.github.com
Accept: */*
```

```
HTTP/1.1 401 Unauthorized
* Server GitHub.com is not blacklisted
Server: GitHub.com
Date: Mon, 28 Sep 2015 19:34:08 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 170
Status: 401 Unauthorized
X-GitHub-OTP: required; sms
X-GitHub-Media-Type: github.v3
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 58
X-RateLimit-Reset: 1443472348
X-XSS-Protection: 1; mode=block
X-Frame-Options: deny
Content-Security-Policy: default-src 'none'
Access-Control-Allow-Credentials: true
Access-Control-Expose-Headers: ETag, Link, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval
Access-Control-Allow-Origin: *
X-GitHub-Request-Id: 598884C4:1768E:32A56D4:56099630
Strict-Transport-Security: max-age=31536000; includeSubdomains; preload
X-Content-Type-Options: nosniff

{
  "message": "Must specify two-factor authentication OTP code.",
  "documentation_url": "https://developer.github.com/v3/auth#working-with-two-factor-authentication"
}
```

#### Request with username and hash as a password (generated from GitHub interface)

```
curl -v -u serbanghita:38aec1da0bx01xe273cfe2cx8xec0ee7f2a5fd91 https://api.github.com/user
```

```
Authorization: Basic c2VyYmFuZ2hpdGE6MzhhZWMxZGEwYjEwMTVlMjczY2ZlMmMyODBlYzBlZTdmMmE1ZmQ5MQ==
User-Agent: curl/7.30.0
Host: api.github.com
Accept: */*
```

```
HTTP/1.1 200 OK
Server: GitHub.com
Date: Mon, 28 Sep 2015 19:42:05 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 1558
Status: 200 OK
X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4999
X-RateLimit-Reset: 1443472925
Cache-Control: private, max-age=60, s-maxage=60
Last-Modified: Mon, 28 Sep 2015 14:57:14 GMT
ETag: "1d7d5861fa1dfc9579e94216b06e114b"
X-OAuth-Scopes: admin:org, admin:public_key, admin:repo_hook, delete_repo, gist, notifications, repo, user
X-Accepted-OAuth-Scopes:
Vary: Accept, Authorization, Cookie, X-GitHub-OTP
X-GitHub-Media-Type: github.v3
X-XSS-Protection: 1; mode=block
X-Frame-Options: deny
Content-Security-Policy: default-src 'none'
Access-Control-Allow-Credentials: true
Access-Control-Expose-Headers: ETag, Link, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval
Access-Control-Allow-Origin: *
X-GitHub-Request-Id: 598884C4:17F5A:7CF94E6:5609980D
Strict-Transport-Security: max-age=31536000; includeSubdomains; preload
X-Content-Type-Options: nosniff
Vary: Accept-Encoding
X-Served-By: d594a23ec74671eba905bf91ef329026

{
  "login": "serbanghita",
  "id": 11x6x4x,
  "avatar_url": "https://avatars.githubusercontent.com/u/11x6x4x?v=3",
  "gravatar_id": "",
  "url": "https://api.github.com/users/serbanghita",
  "html_url": "https://github.com/serbanghita",
  "followers_url": "https://api.github.com/users/serbanghita/followers",
  "following_url": "https://api.github.com/users/serbanghita/following{/other_user}"
  "gists_url": "https://api.github.com/users/serbanghita/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/serbanghita/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/serbanghita/subscriptions",
  "organizations_url": "https://api.github.com/users/serbanghita/orgs",
  "repos_url": "https://api.github.com/users/serbanghita/repos",
  "events_url": "https://api.github.com/users/serbanghita/events{/privacy}",
  "received_events_url": "https://api.github.com/users/serbanghita/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Serban Ghita",
  "company": "Avangate",
  "blog": "http://serban.ghita.org",
  "location": "Bucharest",
  "email": "serbanghita@gmail.com",
  "hireable": null,
  "bio": null,
  "public_repos": 34,
  "public_gists": 1,
  "followers": 133,
  "following": 11,
  "created_at": "2011-10-06T07:24:12Z",
  "updated_at": "2015-09-28T14:57:14Z",
  "private_gists": 4,
  "total_private_repos": 5,
  "owned_private_repos": 5,
  "disk_usage": 44492,
  "collaborators": 2,
  "plan": {
    "name": "micro",
    "space": 976562499,
    "collaborators": 0,
    "private_repos": 5
  }
}
```
