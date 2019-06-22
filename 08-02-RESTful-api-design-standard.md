### RESTful API 设计规范

REST API 是一系列个体可描述 (individually-addressable) 的资源（API的名词）的模型。 资源可以通过他们的资源名称来提及，并可以通过一个小集合内的方法（即API的动词）来操作。

#### 理解Restful

Rest 是 Representational State Transfer缩写，即表现层状态转换。

要理解Restful架构，最好的方法是理解**Representational State Transfer这个词组到底是什么意思，它的每一个词代表了什么涵义**。

##### 资源(Resource)

REST的名称"表现层状态转化"中，省略了主语。"表现层"其实指的是"资源"（Resources）的"表现层"。

**所谓"资源"，就是网络上的一个实体，或者说是网络上的一个具体信息。**它可以是一段文本、一张图片、一首歌曲、一种服务，总之就是一个具体的实在。你可以用一个URI（统一资源定位符）指向它，每种资源对应一个特定的URI。要获取这个资源，访问它的URI就可以，因此URI就成了每一个资源的地址或独一无二的识别符。

所谓"上网"，就是与互联网上一系列的"资源"互动，调用它的URL

##### **表现层（Representation）**

"资源"是一种信息实体，它可以有多种外在表现形式。**我们把"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）。**

比如，文本可以用txt格式表现，也可以用HTML格式、XML格式、JSON格式表现，甚至可以采用二进制格式；图片可以用JPG格式表现，也可以用PNG格式表现。

URI只代表资源的实体，不代表它的形式。严格地说，有些网址最后的".html"后缀名是不必要的，因为这个后缀名表示格式，属于"表现层"范畴，而URI应该只代表"资源"的位置。它的具体表现形式，应该在HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对"表现层"的描述

##### **状态转化（State Transfer）**

访问一个网站，就代表了客户端和服务器的一个互动过程。在这个过程中，势必涉及到数据和状态的变化。

互联网通信协议HTTP协议，是一个无状态协议。这意味着，所有的状态都保存在服务器端。因此，**如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。**

客户端用到的手段，只能是HTTP协议。具体来说，就是HTTP协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：**GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源。**

##### 综述

综合上面的解释，我们总结一下什么是RESTful架构：

　　（1）每一个URI代表一种资源；

　　（2）客户端和服务器之间，传递这种资源的某种表现层；

　　（3）客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

#### 设计指南

##### 协议

API与用户的通信协议，总是使用HTTPs协议

##### 域名

应该尽量将API部署在专用域名之下。

```
https://api.example.com
```

如果确定API很简单，不会有进一步扩展，可以考虑放在主域名下。

```
https://api.example.com
```

##### 版本

应该将API的版本号放入URL。

```
https://api.example.com/v1/
```

另一种做法是，将版本号放在HTTP头信息中，但不如放入URL方便和直观。[Github](https://developer.github.com/v3/media/#request-specific-version)采用这种做法。

还有一种做法是通过媒体类型指定版本信息：

```
Accept: application/vnd.example.com.v1+json
```

其中 `vnd` 表示 `Standards Tree` 标准树类型，有三个不同的树: `x`，`prs` 和 `vnd`。你使用的标准树需要取决于你开发的项目

- 未注册的树（`x`）主要表示本地和私有环境
- 私有树（`prs`）主要表示没有商业发布的项目
- 供应商树（`vnd`）主要表示公开发布的项目

> 后面几个参数依次为应用名称（一般为应用域名）、版本号、期望的返回格式。

至于具体把版本号放在什么地方，这个问题一直存在很大的争议，但由于我们大多数时间都在使用 `Laravel` 开发，`应该` 使用 [dingo/api](https://github.com/dingo/api) 来快速构建应用，它采用第二种方式来管理 `API` 版本，并且已集成了标准的 `HTTP Response`

##### 路径（Endpoint）

路径又称"终点"（endpoint），表示API的具体网址，必需遵守一下规范：

- URL 的命名 `必须` 全部小写
- URL 中资源（`resource`）的命名 `必须` 是名词，并且 `必须` 是复数形式
- `必须` 优先使用 `Restful` 类型的 URL
- URL `必须` 是易读的
- URL `一定不可` 暴露服务器架构

>  至于 URL 是否必须使用连字符（`-`） 或下划线（`_`），不做硬性规定，但 `必须` 根据团队情况统一一种风格。

在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"集合"（collection），所以API中的名词也应该使用复数。

举例来说，有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样。

```
https://api.example.com/v1/zoos
https://api.example.com/v1/animals
https://api.example.com/v1/employees
```

##### URL设计

1. 动词+宾语

   RESTful 的核心思想就是，客户端发出的数据操作指令都是"动词 + 宾语"的结构。比如，`GET /articles`这个命令，`GET`是动词，`/articles`是宾语。

   动词通常就是五种 HTTP 方法，对应 CRUD 操作。

   > - GET：读取（Read）
   > - POST：新建（Create）
   > - PUT：更新（Update）
   > - PATCH：更新（Update），通常是部分更新
   > - DELETE：删除（Delete）

   根据 HTTP 规范，动词一律大写。

2. 动词的覆盖

   有些客户端只能使用`GET`和`POST`这两种方法。服务器必须接受`POST`模拟其他三个方法（`PUT`、`PATCH`、`DELETE`）。

   这时，客户端发出的 HTTP 请求，要加上`X-HTTP-Method-Override`属性，告诉服务器应该使用哪一个动词，覆盖`POST`方法。

   ```
   POST /api/Person/4 HTTP/1.1  
   X-HTTP-Method-Override: PUT
   ```

   上面代码中，`X-HTTP-Method-Override`指定本次请求的方法是`PUT`，而不是`POST`

3. 宾语必须是名词

   宾语就是 API 的 URL，是 HTTP 动词作用的对象。它应该是名词，不能是动词。比如，`/articles`这个 URL 就是正确的，而下面的 URL 不是名词，所以都是错误的。

   ```
   /getAllCars
   /createNewCar
   /deleteAllRedCars
   ```

4. 复数URL

   常见的情况是，资源需要多级分类，因此很容易写出多级的 URL，比如获取某个作者的某一类文章。

   ```
   GET /authors/12/categories/2
   ```

   这种 URL 不利于扩展，语义也不明确，往往要想一会，才能明白含义。

   更好的做法是，除了第一级，其他级别都用查询字符串表达。

   ```
   GET /authors/12?categories=2
   ```

   下面是另一个例子，查询已发布的文章。你可能会设计成下面的 URL。

   ```
   GET /articles/published
   ```

   查询字符串的写法明显更好。

   ```
   GET /articles?published=true
   ```

##### Http动词

对于资源的具体操作类型，由HTTP动词表示。

常用的HTTP动词有下面五个（括号里是对应的SQL命令）。

- GET（SELECT）：从服务器取出资源（一项或多项）。
- POST（CREATE）：在服务器新建一个资源。
- PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
- PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
- DELETE（DELETE）：从服务器删除资源。

还有两个不常用的HTTP动词。

- HEAD：获取资源的元数据。
- OPTIONS：获取信息，关于资源的哪些属性是客户端可以改变的。

下面是一些例子。

- GET /zoos：列出所有动物园
- POST /zoos：新建一个动物园
- GET /zoos/ID：获取某个指定动物园的信息
- PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
- PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
- DELETE /zoos/ID：删除某个动物园
- GET /zoos/ID/animals：列出某个指定动物园的所有动物
- DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物



##### 过滤信息

如果记录数量很多，服务器不可能都将它们返回给用户。API应该提供参数，过滤返回结果。

下面是一些常见的参数。

- ?limit=10：指定返回记录的数量
- ?offset=10：指定返回记录的开始位置。
- ?page=2&per_page=100：指定第几页，以及每页的记录数。
- ?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
- ?animal_type_id=1：指定筛选条件

参数的设计允许存在冗余，即允许API路径和URL参数偶尔有重复。比如，GET /zoo/ID/animals 与 GET /animals?zoo_id=ID 的含义是相同的.

##### 认证

`应该` 使用 `OAuth2.0` 的方式为 API 调用者提供登录认证。`必须` 先通过登录接口获取 `Access Token` 后再通过该 `token` 调用需要身份认证的 `API`。

Oauth 的端点设计示列

- RFC 6749 /token
- Twitter /oauth2/token
- Fackbook /oauth/access_token
- Google /o/oauth2/token
- Github /login/oauth/access_token
- Instagram /oauth/authorize

客户端在获得 `access token` 的同时 `必须` 在响应中包含一个名为 `expires_in` 的数据，它表示当前获得的 `token` 会在多少 `秒` 后失效。

```
{
    "access_token": "token....",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

客户端在请求需要认证的 `API` 时，`必须` 在请求头 `Authorization` 中带上 `access_token`。

```
Authorization: Bearer token...
```

当超过指定的秒数后，`access token` 就会过期，再次用过期/或无效的 `token` 访问时，服务端 `应该` 返回 `invalid_token` 的错误或 `401` 错误码。

```
HTTP/1.1 401 Unauthorized
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache

{
    "error": "invalid_token"
}
```

> Laravel 开发中，`应该` 使用 [JWT](https://github.com/tymondesigns/jwt-auth) 来为管理你的 Token，并且 `一定不可` 在 `api` 中间件中开启请求 `session`。

##### 状态码

服务器向用户返回的状态码和提示信息，常见的有以下一些（方括号中是该状态码对应的HTTP动词）。

- 200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
- 201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
- 202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
- 204 NO CONTENT - [DELETE]：用户删除数据成功。
- 400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
- 401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。
- 403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
- 404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
- 406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
- 410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
- 422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
- 500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。

状态码的完全列表参见[这里](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。

##### 错误处理

如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。

```javascript
{
    error: "Invalid API key"
}
```

##### 返回结果

针对不同操作，服务器向用户返回的结果应该符合以下规范。

- GET /collection：返回资源对象的列表（数组）
- GET /collection/resource：返回单个资源对象
- POST /collection：返回新生成的资源对象
- PUT /collection/resource：返回完整的资源对象
- PATCH /collection/resource：返回完整的资源对象
- DELETE /collection/resource：返回一个空文档

##### Hypermedia API

RESTful API最好做到Hypermedia，即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。

比如，当用户向api.example.com的根目录发出请求，会得到这样一个文档。

```javascript
{"link": {
  "rel":   "collection https://www.example.com/zoos",
  "href":  "https://api.example.com/zoos",
  "title": "List of zoos",
  "type":  "application/vnd.yourformat+json"
}}
```

上面代码表示，文档中有一个link属性，用户读取这个属性就知道下一步该调用什么API了。rel表示这个API与当前网址的关系（collection关系，并给出该collection的网址），href表示API的路径，title表示API的标题，type表示返回类型。

Hypermedia API的设计被称为[HATEOAS](http://en.wikipedia.org/wiki/HATEOAS)。Github的API就是这种设计，访问[api.github.com](https://api.github.com/)会得到一个所有可用API的网址列表。

```javascript
{
  "current_user_url": "https://api.github.com/user",
  "authorizations_url": "https://api.github.com/authorizations",
  // ...
}
```

上面可以看到，如果想获取当前用户的信息，应该去访问[api.github.com/user](https://api.github.com/user)，然后就得到了下面结果。

```javascript
{
  "message": "Requires authentication",
  "documentation_url": "https://developer.github.com/v3"
}
```

上面代码表示，服务器给出了提示信息，以及文档的网址。

##### 误区

RESTful架构有一些典型的设计误区。

**最常见的一种设计错误，就是URI包含动词。**因为"资源"表示一种实体，所以应该是名词，URI不应该有动词，动词应该放在HTTP协议中。

举例来说，某个URI是/posts/show/1，其中show是动词，这个URI就设计错了，正确的写法应该是/posts/1，然后用GET方法表示show。

如果某些动作是HTTP动词表示不了的，你就应该把动作做成一种资源。比如网上汇款，从账户1向账户2汇款500元，错误的URI是：

```
POST /accounts/1/transfer/500/to/2
```

正确的写法是把动词transfer改成名词transaction，资源不能是动词，但是可以是一种服务：

```
POST /transaction HTTP/1.1
Host: 127.0.0.1

from=1&to=2&amount=500.00
```

##### 其他

服务器返回的数据格式，应该尽量使用JSON，避免使用XML。