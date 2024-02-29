## `vue`的响应式



- 组件data的数据一旦变化，立刻触发视图更新
- 实现数据驱动视图的第一步
  - `object.defineProperty`(`vue2`)
  - `Proxy`(`vue3`)
- `object.defineProperty`的 `set`方法可以监听数据修改



### `object.defineProperty`缺点

- 深度监听，需要递归到底，一次性计算量大
- 无法监听新增，删除



`object.defineProperty`监听数组需要特殊处理（`object.create`重新定义数组）





## `VDom` 和 `diff` 算法

参考`snabbdom` 学习`vdom`

首先`vdom` 是指虚拟`dom`，是`virtual DOM` 的缩写，`VDom`展示如下

```html
<div id='div1' class='container'>
    <p>vdom</p>
    <ul style='font-size:20px'>
        <li>a</li>
    </ul>
</div>
```

以上`html` 代码转换为 `vdom`代码如下所示

```json
{
    tag:'div',
    props:{
        className:'container',
        id:'div1'
    },
    children:[
        {
            tag:'p',
            text:'vdom'
        },
        {
            tag:'ul',
            props:{
                style:'font-size:20px',
            },
            children:[
                {
                    tag:'li',
                    text:'a'
        		}
            ]
        }
    ]
}
```

为什么会出现`diff`算法：

- 首先，传统`dom`操作，比如`js`，`jq`，在进行添加等操作，会统一刷新列表
- `diff`下的`vdom`，则会进行局部更新（一个列表下，修改哪项更新哪项，不会统一刷新列表）



`diff` 比对规则

- 只比较同一层级，不跨级比较
- `tag`不相同，则直接删除重建，不在深度比较
- `tag`和`key`，如果都相同，则认为相同节点，不做深度比较





为什么组件`data`必须是一个函数

- 不是函数，会造成实例化数据共享
- 定义函数后，在闭包执行，就不会共享