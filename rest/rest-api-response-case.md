###Restful API 응답 케이스 예제
--- 
####User Data
```
[
    {
        "name" : "John"
        , "id" : 1
    } ,
    {
        "name" : "Albert"
        , "id" : 2
    } ,
    {
        "name" : "Cathy"
        , "id" : 3
    } ,
    {
        "name" : "Johnson"
        , "id" : 4
    } 
]
```


---
#####GET /users
```
* Data Exist
- Response : 200 Ok
- Response Body :
[
    {
        "name" : "John"
        , "id" : 1
    } ,
    {
        "name" : "Albert"
        , "id" : 2
    } ,
    {
        "name" : "Cathy"
        , "id" : 3
    }
    {
        "name" : "Johnson"
        , "id" : 4
    } 
]
```

```
* If Data Empty
- Response : 200 Ok
- Response Body :
[]
```

---

#####GET /users?name=John
```
- Response : 200 Ok
- Response Body :
    {
        "name" : "John"
        , "id" : 1
    } ,
    {
        "name" : "Johnson"
        , "id" : 4
    } 
]
```
#####GET /users?name=Eldie
```
- Response : 200 Ok
- Response Body :
[]
```

---

#####GET /users/1
```
- Response : 200 Ok
- Response Body :
{
    "name" : "John"
    , "id" : 1
} 
```

#####GET /users/10
```
- Response : 404 Not Found
- Response Body :
{
    "code" : 1234
    , "message" : "can not found User" 
    (, "userMessage" : "해당 사용자를 찾을 수 없습니다.")
}
```



#####POST /users {"name":"Larry"}
```
- Response : 201 Created
- Response Header :
Location : /users/5
```

```
- Response : 200 Ok
- Response Body :
{
    "name" : "Larry"
    , "id" : 5
}
```



--- 
###Error

```
- Response : 4xx [description]
- Response Body :
{
    "code" : [error detail code]
    , "message" : [error message] 
    (, "userMessage" : [error message for user])
}
```

--- 
