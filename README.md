# RESTful
RESTful API learning

## Restful learning

#### 什么是Restful Api
- **名称：** 

    REST，即Representational State Transfer的缩写。翻译为**表现层状态转化**，更清楚的理解应该是**资源在网络中以某种表现形式进行状态转移**。
    
    REST是所有Web应用都应该遵守的架构设计指导原则。
    
    REST可以看着是http协议的一种直接应用。
            
    如果一个架构符合REST原则，就称它为**RESTful架构**。
    
    Rest主体是**资源**（resources）,Restful实际就是面向资源的一种架构，URI代表资源的位置，也就是资源本身。
    
    **表现层**（Representation），是把“资源”具体呈现出来的形式，URI只代表资源的实体，不代表它的形式。严格地说，有些网址最后的".html"后缀名是不必要的，因为这个后缀名表示格式，属于"表现层"范畴，而URI应该只代表"资源"的位置。它的具体表现形式，应该在HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对"表现层"的描述。
    
    **状态转化**（State Transfer），互联网通信协议HTTP协议，是一个无状态协议。这意味着，所有的状态都保存在服务器端。因此，如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。
- **起源：**
    
    REST这个词，是Roy Thomas Fielding在他2000年的博士论文中提出的。
    
    Fielding是一个非常重要的人，他是HTTP协议（1.0版和1.1版）的主要设计者、Apache服务器软件的作者之一、Apache基金会的第一任主席。所以，他的这篇论文一经发表，就引起了关注，并且立即对互联网开发产生了深远的影响。

    他这样介绍论文的写作目的：
    >"本文研究计算机科学两大前沿----软件和网络----的交叉点。长期以来，软件研究主要关注软件设计的分类、设计方法的演化，很少客观地评估不同的设计选择对系统行为的影响。而相反地，网络研究主要关注系统之间通信行为的细节、如何改进特定通信机制的表现，常常忽视了一个事实，那就是改变应用程序的互动风格比改变互动协议，对整体表现有更大的影响。我这篇文章的写作目的，就是想在符合架构原理的前提下，理解和评估以网络为基础的应用软件的架构设计，得到一个功能强、性能好、适宜通信的架构。"
 
    > (This dissertation explores a junction on the frontiers of two research disciplines in computer science: software and networking. Software research has long been concerned with the categorization of software designs and the development of design methodologies, but has rarely been able to objectively evaluate the impact of various design choices on system behavior. Networking research, in contrast, is focused on the details of generic communication behavior between systems and improving the performance of particular communication techniques, often ignoring the fact that changing the interaction style of an application can have more impact on performance than the communication protocols used for that interaction. My work is motivated by the desire to understand and evaluate the architectural design of network-based application software through principled use of architectural constraints, thereby obtaining the functional, performance, and social properties desired of an architecture. )

- **模式：**
    
    `http(s)://server.com/app-name/{version}/{domain}/{rest-convention}`

#### 如何设计RESTful API
- 协议：API与用户的通信协议，总是使用**HTTPs协议**。
- 域名：应该尽量将API部署在专用域名之下。
    > https://api.example.com
- 版本：应该将API的版本号放入URL。
    > https://api.example.com/v1/
- 路径：URI中不能出现动词，只能有名词，名词推荐使用复数。
    > https://api.example.com/v1/employees
- HTTP动词：对于资源的具体操作类型，由HTTP动词表示，根据 HTTP 规范，动词一律大写。
    + 常用的动词有：
    > - GET（SELECT）：从服务器取出资源（一项或多项）。（幂等且安全）
    > - POST（CREATE）：在服务器新建一个资源。  （不幂等也不安全）
    > - PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源，全部信息）。 （幂等但不安全）
    > - PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性，部分信息）。 （不幂等也不安全）
    > - DELETE（DELETE）：从服务器删除资源。 （幂等但不安全）
    > - HEAD：获取资源的元数据。 （幂等且安全）
    > - OPTIONS：获取信息，关于资源的哪些属性是客户端可以改变的。
    
    + 例子：
    > - GET /zoos：列出所有动物园
    > - POST /zoos：新建一个动物园
    > - GET /zoos/ID：获取某个指定动物园的信息
    > - PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
    > - PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
    > - DELETE /zoos/ID：删除某个动物园
    > - GET /zoos/ID/animals：列出某个指定动物园的所有动物
    > - DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物

- 过滤信息（Filtering）：
    > * ?limit=10：指定返回记录的数量
    > * ?offset=10：指定返回记录的开始位置。
    > * ?page=2&per_page=100：指定第几页，以及每页的记录数。
    > * ?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
    > * ?animal_type_id=1：指定筛选条件
  
- 状态码（Status Codes）：服务器向用户返回的状态码和提示信息
    状态码的详细信息通过网络资源自行查找
    
- 错误处理（Error handling）：
     
     `{
           error: "Invalid API key"
       }`

- 返回结果：针对不同操作，服务器向用户返回的结果应该符合以下规范。
    > - GET /collection：返回资源对象的列表（数组）
    > - GET /collection/resource：返回单个资源对象
    > - POST /collection：返回新生成的资源对象
    > - PUT /collection/resource：返回完整的资源对象
    > - PATCH /collection/resource：返回完整的资源对象
    > - DELETE /collection/resource：返回一个空文档
    
- Hypermedia API

- 接口返回模式：采用固定的数据格式封装

    `{
        status:0, 
        data:{}||[], 
        msg:’’ 
        }
    `

##### RESTful API设计
- 资源路径
- URL结尾不应该包含斜杠“/”
- 正斜杠分隔符”/“**必须**用来指示层级关系
    > 例如：
      
      http://api.user.com/schools/grades/classes/boys 
- 应该使用连字符”-“来提高URL的可读性，而不是使用下划线”_”
- URL路径中首选小写字母
- URL路径名词均为复数
- RESTful API对资源的操作,由HTTP动词表示
- CURD操作
- 资源过滤
- 返回状态码推荐标准HTTP状态码

#### 安全性和幂等性
1. 安全性：不会改变资源状态，可以理解为只读的；
2. 幂等性：执行1次和执行N次，对资源状态改变的效果是等价的。
3. GET，HEAD, PUT, DELETE一定要设计成等幂的

##### 如何设计符合幂等性的高质量RESTful API
- **HTTP GET方法 vs HTTP POST方法**
也许，你会想起一个面试题。HTTP请求的GET与POST方式有什么区别？你可能会回答到：GET方式通过URL提交数据，数据在URL中可以看到；POST方式，数据放置在HTML HEADER内提交。但是，我们现在从RESTful的资源角度来看待问题，HTTP GET方法是幂等的，所以它适合作为查询操作，HTTP POST方法是非幂等的，所以用来表示新增操作。
      
但是，也有例外，我们有的时候可能需要把查询方法改造成HTTP POST方法。比如，超长（1k）的GET URL使用POST方法来替代，因为GET受到URL长度的限制。虽然，它不符合幂等性，但是它是一种折中的方案。
      
- **HTTP POST方法 vs HTTP PUT方法**
对于HTTP POST方法和TTP PUT方法，我们一般的理解是POST表示创建资源，PUT表示更新资源。当然，这个是正确的理解。
      
但是，实际上，两个方法都用于创建资源，更为本质的差别是在幂等性。HTTP POST方法是非幂等，所以用来表示创建资源，HTTP PUT方法是幂等的，因此表示更新资源更加贴切。
      
- **HTTP PUT方法 vs HTTP PATCH方法**
此时，你看会有另外一个问题。HTTP PUT方法和HTTP PATCH方法，都是用来表述更新资源，它们之间有什么区别呢？我们一般的理解是PUT表示更新全部资源，PATCH表示更新部分资源。首先，这个是我们遵守的第一准则。根据上面的描述，PATCH方法是非幂等的，因此我们在设计我们服务端的RESTful API的时候，也需要考虑。如果，我们想要明确的告诉调用者我们的资源是幂等的，我的设计更倾向于使用HTTP PUT方法。
      



#### 参考
* [理解RESTful架构 ](http://www.ruanyifeng.com/blog/2011/09/restful.html) [作者： 阮一峰]
* [RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html) [作者： 阮一峰]
* [RESTful API 最佳实践](http://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html) [作者： 阮一峰]
* [百度百科](https://baike.baidu.com/item/RESTful/4406165?fr=aladdin)
* [状态码大全](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)
* [wiki状态码](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
* [RESTful API规范（详细版）](https://blog.csdn.net/qq_37257657/article/details/81206520)
* [如何理解RESTful的幂等性](https://blog.csdn.net/garfielder007/article/details/55684420)
