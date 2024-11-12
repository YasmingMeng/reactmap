<!--
 * @Description:
 * @Date: 2024-11-06 16:38:04
 * @LastEditTime: 2024-11-12 17:33:00
-->

## mutating data（更改数据）

### Server action（服务器操作）

1. allow user to run async code directly on the server.
2. asynchronous function can excute on the Server and can be invoked form client or Server component.
3. Server action are deeply integrated with Next.Js

### <form> element (<form>组件)

1. `action` attribute can automatically reveive the naitve `FromData` Object
2. if Javascript disabled on the client but forms still work
3. use `revalidatePath` and `revalidateTag` APIs to revalidate the associated cache

### Use

1. By adding the `use server` in ts file, all the export file within the ts file will mark as Server Action.
2. Next.js has Client-side Routed cache that stores the route segments in the user's browser for a time

## Create Dynamic Route Seagment

1. Next.js allows users to create dynamic route segments by wrapping a folder name in square brackets, such as [id], to reflect parameters in the route name.
