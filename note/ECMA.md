#### 字符串中的方法

1. charAt(索引值) //表示从字符串中把索引对应的字符，获取出来
2. toUpperCase()把值转换成大写
3. slice()截取字符串，从指定索引往后截取



#### 数组中的方法

some方法，从数组里面找元素，找到后终止

```js
const arr = ['小红', '你大红', '苏大强', '宝']
forEach 循环一旦开始，无法在中间被停止
   arr.forEach((item, index) => {
      console.log('object')
      if (item === '苏大强') {
        console.log(index)
      }
    })
```

```js
const arr = ['小红', '你大红', '苏大强', '宝']
arr.some((item, index) => {
      console.log('ok')
      if (item === '苏大强') {
        console.log(index)
        // 在找到对应的项之后，可以通过 return true 固定的语法，来终止 some 循环
        return true
      }
    })
```



every方法

```js
const arr = [
      { id: 1, name: '西瓜', state: true },
      { id: 2, name: '榴莲', state: false },
      { id: 3, name: '草莓', state: true },
    ]

    // 需求：判断数组中，水果是否被全选了！
    const result = arr.every(item => item.state)
    console.log(result)
```



reduce方法，循环数组每一项的累加到累加结果

```js
const arr = [
      { id: 1, name: '西瓜', state: true, price: 10, count: 1 },
      { id: 2, name: '榴莲', state: false, price: 80, count: 2 },
      { id: 3, name: '草莓', state: true, price: 20, count: 3 },
    ]

    // 需求：把购物车数组中，已勾选的水果，总价累加起来！
    /* let amt = 0 // 总价
        arr.filter(item => item.state).forEach(item => {
          amt += item.price * item.count
        })
    
        console.log(amt) */

    // arr.filter(item => item.state).reduce((累加的结果, 当前循环项) => { }, 初始值)
    const result = arr.filter(item => item.state).reduce((amt, item) => amt += item.price * item.count, 0)

    console.log(result)
```



filter方法

push方法

findIndex

splice







#### 数字中的方法

Number.toFixed(n) 保留n位小数



































