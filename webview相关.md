## webview 相关

- #### 手机版网页不能缩放的问题

  手机版网页即便设置 *setSupportZoom(true)* 之后，依然不能进行缩放

  以<https://m.baidu.com>为例，可以在网页源码看到如下代码

  ```html
  <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
  ```

  这就是控制缩放的代码了

  - *minimum-scale=1.0* 最小缩放倍数
  - *maximum-scale=1.0* 最大缩放倍数
  - *user-scalable=no* 是否允许缩放

  所以解决方案无非就是修改这几个参数，**通过向网页中注入js代码修改这个节点中的 *content* 属性**

  js 代码如下：

  ````javascript
  var vts = document.getElementsByName('viewport')
  if (vts.length > 0) {
      vts[0].setAttribute('content','width=device-width,minimum-scale=1.0,maximum-scale=4.0,user-scalable=yes');
  }
  ````