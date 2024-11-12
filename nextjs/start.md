<!--
 * @Description:
 * @Date: 2024-06-25 12:21:40
 * @LastEditTime: 2024-06-25 17:05:45
-->

### 文件夹结构

- `/app`：包含应用程序的所有路线、组件和逻辑，这是您主要进行工作的地方。
- `/app/lib`：包含应用程序中使用的函数，例如可重用的实用程序函数和数据提取函数。
- `/app/ui`：包含应用程序的所有 UI 组件，例如卡片、表格和表单。为了节省时间，我们已为您预先设计了这些组件的样式。
- `/public`：包含应用程序的所有静态资产，例如图像。
- 配置文件：您还会注意到配置文件，例如 next.config.js 位于应用程序根目录的文件。大多数此类文件都是在您使用 启动新项目时创建和预配置的 create-next-app。您无需在本课程中修改它们。

### css 样式添加

#### 全局样式

- `/app/ui`文件夹下添加`global.css`文件，添加全局 css 样式规则。
- 通过导航`/app/layout.tsx`并导入`global.css`文件将全局样式添加到您的应用程序.

```tsx
import '@/app/ui/global.css'

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

#### css modoules

- `css modules`可以允许通过创建**唯一的类名**将样式限制在组件中，避免造成样式的冲突问题。
- Next.js 通过 [name.module.css] 文件命名约定来支持 CSS 模块 。

#### 使用 clsx 切换 cs 的库名称

- 官方文档 [https://github.com/lukeed/clsx]
