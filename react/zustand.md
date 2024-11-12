<!--
 * @Description:
 * @Date: 2024-08-01 13:03:25
 * @LastEditTime: 2024-08-04 12:37:07
-->

## 主要的 APi

1. **create**

- create 函数支持三个参数
  1. 第一个参数：`(set、get、api)=>{...}`
  2. 第二个参数是布尔值，调用 create 修改状态的方法后返回的状态值，当传值为 false 时，该状态值会与 create 方法的原状态进行合并；若值为 true 时，该状态值会直接覆盖原状态值。
