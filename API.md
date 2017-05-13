
#   API 设计
RESTful API 设计简介:
simulay 不仅仅是一个在线仿真系统, 同时也有对外提供接口服务的能力, 整套 API 的设计参考
REST架构风格的 API 设计规范,
REST（英文：Representational State Transfer，又称具象状态传输）是Roy Thomas Fielding博士于2000年在他的博士论文
[
 Fielding, Roy Thomas. Chapter 5: Representational State Transfer (REST). Architectural Styles and the Design of Network-based Software Architectures (Ph.D.). University of California, Irvine. 2000. This chapter introduced the Representational State Transfer (REST) architectural style for distributed hypermedia systems. REST provides a set of architectural constraints that, when applied as a whole, emphasizes scalability of component interactions, generality of interfaces, independent deployment of components, and intermediary components to reduce interaction latency, enforce security, and encapsulate legacy systems.] 

 中提出来的一种万维网软件架构风格，目的是便于不同软件/程序在网络（例如互联网）中互相传递信息。
主要有三大特点

*    资源是由URI来指定。
*   对资源的操作包括获取、创建、修改和删除资源，这些操作正好对应HTTP协议提供的GET、POST、PUT和DELETE方法。
*   通过操作资源的表现形式来操作资源。


### 数据读取API
| Action                              | Method | Route         | Requires token |
|:------------------------------------|:-------|:--------------|:---------------|
| [List runner](list_runner.md)   | GET    | /runner     | Optional       |
| [Get runner](get_runner.md)       | GET    | /runner/:id | No             |
| [Update runner](update_runner.md) | PUT    | /runner/:id | Yes            |
| [Delete runner](delete_runner.md) | DELETE | /runner/:id | Yes            |
| [Get result](get_runner.md)       | GET    | /runner/:id/result | No             |
| [Get analysis](get_runner.md)       | GET    | /runner/:id/analysis | No             |



##### Get runner
    curl --request GET \
         --url 'HTTPS://simulay.outshine.me/runner/e2tx9nh4fh'

### Example response data
    {
      "id": "e2tx9nh4fh",
      "url": "HTTPS://simulay.outshine.me/runner/e2tx9nh4fh",
      "created": "2017-04-23T22:03:11Z",
      "modified": "2017-04-23T22:03:11Z",
      "hash": "9bdd2b79fafbf81313a79b1df1be5c2671422307",
      "language": "octave",
      "title": "main",
      "public": true,
      "owner": "anonymous",
      "files": [
        {
          "name": "main.m",
          "content": "2+2
        }
      ],
      result_id: '23423423',
      analysis_id: '23424251',
    }



##   仿真runnerAPI
| Action                              | Method | Route                         | Requires token |
|:------------------------------------|:-------|:------------------------------|:---------------|
| [List languages](list_languages.md) | GET    | /languages                    | No             |
| [List versions](list_versions.md)   | GET    | /languages/:language          | No             |
| [Run code](run.md)                  | POST   | /languages/:language/:version | Yes            |



## Run code

##### Run code
```bash
curl --request POST \
     --header 'Authorization: Token 0123456-789a-bcde-f012-3456789abcde' \
     --header 'Content-type: application/json' \
     --data '{"files": [{"name": "main.m", "content": "2+2"}]}' \
     --url 'https://run.glot.io/languages/octave/latest'
```


## Example data

### Simple example
##### Request
```javascript
{
  "files": [
    {
      "name": "main.m",
      "content": "2+2"
    }
  ]
}
```

##### Response
```javascript
{
  "stdout": "4",
  "stderr": "",
  "error": ""
}
```
