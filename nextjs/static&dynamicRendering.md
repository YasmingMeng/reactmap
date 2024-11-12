## static rendering（静态渲染）

- 通过静态渲染，时数据获取和渲染发生在服务构建时或数据重新验证时。
- 静态渲染的优点：

  1. 网站更快
     - 预渲染的内容可以缓存并全球分发，保证用户获取网站内容更快的同时，也保证了内容的可靠性。（原理？）
  2. 减少数据过载
     - 因为预渲染的内容可以缓存下来，所以不需为用户的每个请求去动态生成内容。
  3. 优化搜索引擎
     - pre-rendered content is easier for search engine crawlers to index, so the content is already avaliable when it loads, this can improve search engine rankings.
- static rendering is useful for thoese do not need dynamic generate content UI such as Product Page or static blog post which the content is prepared



## Dynamic Rendering(动态渲染)

- content is rendered on the server when each ueser at quest time with Dynamic rendering.

- dynamic rendering benefit:

  1. Real-Time Data(实时数据):
     - Users can get the real-time data or frequently renew application data, dynamic rendering is more fit those  applications where data change often.

  2. User-Specific Content(用户定制数据):
     - It fits to serve personalized data, such as dashboards and user profiles, or generate content based on user interaction

  3. Request Time Infomation(请求时间信息):
     - with dynamic rendering, websites can store information that only to know when request happen, such as cookies or url search parameters