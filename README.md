 ## 深入面试
 ### 一、HTML5、CSS3的特性分别是？
1. HTML5的目的是为了创建更简单的web程序，书写更简洁的HTML代码。
2. 同样的功能只要使用元素的属性标签就可以实现 ，非常清楚，容易实现，简洁易懂。
3. HTML5 ≈ HTML4+CSS2+JS 更加语义化的结构标签，用标签代替css+脚本js。
4. HTML设计原则
   - 兼容性：老版本浏览器正常运行 迭代性质，又不影响正常使用。
   - 实用性：简单实用的功能 能够解决实际问题，丰富web应用。
   - 非革命性发展：发展性的，并不是推到重来，而是在原有的基础上做加工，做迭代，更易于使用，更方便使用。
5. HTML5要解决的三个问题
   - 兼容不同浏览器，统一规范。
   - 规范文档结构。
   - 增加web应用功能，实现富web应用。
6. CSS3能做什么？
   - 模块与模块结构化，basic box model、Line、Text、Color等，减少浏览器不完全支持的可能性。
   - 能够增加在CSS2中没有办法解决的样式。
   - 在CSS2的基础上添加和完善更多的功能。
### 二、正则表达式、面向对象、字符串函数，常用的有哪些
### 三、HTTP请求包包含哪些内容
### 四、怎么设置HTTP请求HEARD
### 五、jquery和Bootstrap用过多久？现在是否还在使用？
### 六、闭包的理解
- 闭包的定义很简单：函数 A 返回了一个函数 B，并且函数 B 中使用了函数 A 的变量，函数 B 就被称为闭包。
``` javascript
function A() {
  let a = 1
  function B() {
      console.log(a)
  }
  return B
}
```
- 你是否会疑惑，为什么函数 A 已经弹出调用栈了，为什么函数 B 还能引用到函数 A 中的变量。因为函数 A 中的变量这时候是存储在堆上的。现在的 JS 引擎可以通过逃逸分析辨别出哪些变量需要存储在堆上，哪些需要存储在栈上。
### 七、vue中用computed简单实现数据的双向绑定（getter 和 setter）
- 主要实现的效果：

1. 改变 姓、名 两个输入框的内容时，姓-名、姓-名（双向绑定）这两个输入框内的值将会更新；

2. 改变 姓-名 这个输入框中的内容时，姓、名输入框的内容不会更新；

3. 改变 姓-名（双向绑定）这个输入框中的内容时，姓、名输入框的内容会同步更新（实现了数据的双向绑定，至于 姓-名 这个输入框中的内容改变了，那是因为 姓、名 这两个输入框导致的）。

- 注意：
1. getter 和 setter 只是一个概念，并不是两个实际的方法，

2. getter对应的是get方法，即 获取对应的值 时候调用的回调函数

3. setter对应的是set方法，即 监听对应的值的改变 时候调用的回调函数（注意：不是设置，不是设置，不是设置！！！）；并且 set 接受一个参数，即改变后的值。

4. 计算属性（在使用get和set的时候）使用了箭头函数，则this不会指向这个组件的实例；如果你必须使用箭头函数，只有将其实例作为函数的第一个参数来访问 即： vm => vm.a * 2

``` javascript
<template>
    <!-- computed 实现双向绑定 -->
    <div class="twoWayBind">
        <!-- 姓 -->
        <p>
            <span class="title">姓：</span>
            <input type="text" class="firstName" v-model="firstName">            
        </p>
 
        <!-- 名 -->
        <p>
            <span class="title">名：</span>
            <input type="text" class="lastName" v-model="lastName">
        </p>       
 
        <!-- 显示“姓-名”； 修改后姓、名输入框的内容不会更新 -->
        <p>            
            <span class="title">姓-名：</span>
            <input type="text" class="fullName" v-model="fullName">
            <span class="promptCon">显示“姓-名”； 修改后姓、名输入框的内容不会更新</span>
        </p>
 
        <!-- 显示“姓-名”； 修改后姓、名输入框的内容会同步更新 -->
        <p>
            <span class="title">姓-名（双向绑定）：</span>
            <input type="text" class="fullName2" v-model="fullName2">
            <span class="promptCon">显示“姓-名”； 修改后姓、名输入框的内容会同步更新</span>
        </p>
    </div>
</template>
 
<script>
export default {
    name: 'TwoWayBind',
    data(){
        return{
            firstName: 'A',
            lastName: 'B',
        }
    },
    computed: {
        fullName() {
            return this.firstName + "-" + this.lastName;
        },
        fullName2: {
            // 注意这里不能使用箭头函数，官网解释：计算属性使用了箭头函数，则this不会指向这个组件的实例，
            //                      不过你仍然可以将其实例作为函数的第一个参数来访问  即： vm => vm.a * 2
            get: function () {     
                return this.firstName + "-" + this.lastName;
            },
            set: function (value){      //value为用户修改fullName2后的值
                const names = value.split('-');
                this.firstName = names[0];      //注意：这样修改了firstName和lastName的值，会导致fullName也跟着变化
                this.lastName = names[1];
            }
        }
    }
}
</script>
 
<style lang="scss" scoped>
.twoWayBind{
    p{
        margin: 10px 0px;
        display: flex;
        flex-direction: flex-start;
        .title{
            display: inline-block;
            width: 150px;
            text-align: center;
        }        
        input{
            padding: 0px 6px;
        }
        .promptCon{
            color: #aaa;
            margin-left: 10px;
        }
    }
}
 
</style>
```