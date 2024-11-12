## 获取数据库数据的方法

### API 层(API layer)

- **api**是代码和数据库的**中间件**，在 nextJs 中，可以使用[router Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)创建 API。
  - u can create an custom request by use router handlers for a given router , and using Web request and response APIs
  - 支持 GET、POST、PUT、PATCH、DELETE、HEAD 和 OPTIONS 的 http 方法。如果调用不支持的方法，nextJS 将会返回 405.

### 数据库请求(database require)

- 使用 SQL 或者[ORM](https://vercel.com/docs/storage/vercel-postgres/using-an-orm)与数据库交互

### 使用服务器组件访问数据

- **nextJs**默认使用 react serve components。
  - react serve components 可以在不使用`Useeffect`,`UseState`或者数据获取库的情况下，使用`async/await`来异步获取数据。同时该组件支持 Promise 语法糖。
  
    - tsx需要使用async导出异步组件，组件内就可以使用await来获取数据（fetch data）
  
      ```tsx
      export default async function Page() {
      //代码
      }
      ```
  
  - serve components 可以在服务端运行逻辑和数据获取，只将结果发送到客户端。
  
  - 不用额外使用 API 层，直接访问数据库。

### SQL 语句

- 使用 [Vercel Postgres SDK](https://vercel.com/docs/storage/vercel-postgres/sdk)和SQL编写sql查询来与数据库交互。

- 当你同步执行接口请求，可能会导致请求相互阻塞，导致请求瀑布

  ```ts
  const revenue = await fetchRevenue();
  const latestInvoices = await fetchLatestInvoices(); // wait for fetchRevenue() to finish
  const {
    numberOfInvoices,
    numberOfCustomers,
    totalPaidInvoices,
    totalPendingInvoices,
  } = await fetchCardData(); // wait for fetchLatestInvoices() to finish
  ```

  - 什么是**请求瀑布（request waterfalls）**？
    - 瀑布是一系列依赖前置请求完成的请求序列，只要一个请求阻塞或者还未返回数据，后置的请求就无法执行。

### 并行获取数据（Parallel fetch data）

- 并行请求数据，在同一时间初始化所有请求数据可以避免请求瀑布。
  - 使用`Promise.all`和`Promise.allsettled`同时初始化请求

```ts
{
  try {
    // You can probably combine these into a single SQL query
    // However, we are intentionally splitting them to demonstrate
    // how to initialize multiple queries in parallel with JS.
    const invoiceCountPromise = sql`SELECT COUNT(*) FROM invoices`;
    const customerCountPromise = sql`SELECT COUNT(*) FROM customers`;
    const invoiceStatusPromise = sql`SELECT
         SUM(CASE WHEN status = 'paid' THEN amount ELSE 0 END) AS "paid",
         SUM(CASE WHEN status = 'pending' THEN amount ELSE 0 END) AS "pending"
         FROM invoices`;
	//并行初始化所有请求	
    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);

    const numberOfInvoices = Number(data[0].rows[0].count ?? '0');
    const numberOfCustomers = Number(data[1].rows[0].count ?? '0');
    const totalPaidInvoices = formatCurrency(data[2].rows[0].paid ?? '0');
    const totalPendingInvoices = formatCurrency(data[2].rows[0].pending ?? '0');

    return {
      numberOfCustomers,
      numberOfInvoices,
      totalPaidInvoices,
      totalPendingInvoices,
    };
}
  
```

