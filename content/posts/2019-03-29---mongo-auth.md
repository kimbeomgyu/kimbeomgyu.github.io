---
title: mongoDB 권한 설정하는 방법
date: '2019-03-29T20:09'
template: 'post'
draft: false
slug: '/posts/4/'
category: 'database'
tags:
  - 'database'
  - 'mongodb'
  - 'auth'
description: 'mongoDB에서 권한 설정하는 방법'
---

<h4>사용자 목록 확인</h4>

`use admin`

`show users`

<h4>모든 데이터베이스내의 사용자</h4>

`use admin`

`cur = db.system.users.find()`

`cur.count()`

<h4>계정생성</h4>

`db.createUser` 해당 데이터베이스의 유저객체를 생성한다.

- 관리자 계정 생성 예시

```javascript
use test
db.createUser( {user: "testUser",
    pwd: "test",
    roles: ["readWrite", "dbAdmin"] } )
```

- 읽기권한, 특정 데이터베이스 읽고쓰기 권한 계정 생성 예시

```javascript
use admin
db.createUser( {user: "testUser",
    userSource: "test",
    roles: ["read"],
    otherDBRoles:{ testDB2: ["readWrite"] } } )
```

<h4>사용자 삭제</h4>

`db.dropUser` 해당 데이터베이스의 유저객체를 삭제한다.

- 삭제 예시

```javascript
  use testDB
  db.dropUser("testUser")
```

<h4>사용자 관리자 계정 생성</h4>

사용자 관리자는 데이터베이스나 다른 관리 기능을 운영하는 권한 말고 사용자를 생성할 수 있는 권한만 갖고 있어야 한다.

- 사용자를 생성하는 권한을 가진 계정 예시

  ```javascript
  use admin
  db.createUser({ user: "useradmin",
  pwd: "test",
  roles: ["userAdminAnyDatabase"]
  })
  ```

<h4>인증</h4>

—auth 파라미터를 사용해서 재시작해야한다.

`mongod -dbpath </data/db> —auth`

이후부터는 접근하기 위해 사용자와 패스워드를 이용해야 한다. 아니면 접속 후 명령어를 통해 로그인해야한다.

```javascript
use admin
db.auth("useradmin","password")
```

<h4>권한 설정후 접속방법</h4>

`mongo <host:port> -u <user> -p <pwd> --authenticationDatabase <database>`

<h4>또다른 권한 방법</h4>

```javascript
//루트계정생성
> use admin
> db.createUser({user: "ROOT_ID", pwd: "ROOT_PASSWO", roles:["root"]})
//재시작
$ sudo service mongod restart
$ mongo
> mongo <host:port> -u "ROOT_ID" -p "ROOT_PASSWO" --authenticationDatabase "admin"

//데이터베이스계정생성
> use DATABASE
> db.createUser({user: "DB_USER_ID", pwd: "DB_USER_PASSWORD", roles:["dbOwner"]})
//재접속
> mongo <host:port/DATABASE> -u "DB_USER_ID" -p "DB_USER_PASSWORD"

```
