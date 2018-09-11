# HelloWorld

### **如何实现事件委托**
- 事件委托，就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。
```
//在ul中添加事件，点击li标签，打印出对应标签内的内容
<ul id="ul1">
    <li>111</li>
    <li>222</li>
    <li>333</li>
    <li>444</li>
</ul>
<script>
    window.onload = function(){
        var oUl = document.getElementById("ul1");
        oUl.onclick = function(ev){
            var ev = ev || window.event;
            var target = ev.target || ev.srcElement;
            if(target.nodeName.toLowerCase() == 'li'){
                alert(target.innerHTML);
            }
        }
    }
</script>
```
### **ES6的新特性**
- 块级区域。let声明变量，const声明只读常量。
```
{   
    let a = 10;   
    var b = 1; 
}  
a // ReferenceError: a is not defined. 
b // 1
```
- 模板字符串。
```
// 字符串中嵌入变量 
let name = "Bob", time = "today"; 
`Hello ${name}, how are you ${time}?`
```
- 箭头函数。
```
var f = v => v;
// 等同于 
var f = function (v) {   return v; };
```
- export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到export default命令，为模块指定默认输出。
```
// 第一组 
export default function crc32() { // 输出 // ... } 
import crc32 from 'crc32'; // 输入 
// 第二组 
export function crc32() { // 输出 // ... }; 
import {crc32} from 'crc32'; // 输入
```
- 上面代码的两组写法，第一组是使用export default时，对应的import语句不需要使用大括号；第二组是不使用export default时，对应的import语句需要使用大括号。
export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能唯一对应export default命令。
#### import 和 export，导入的时候有没有大括号的区别
1. 当用export default people导出时，就用 import people 导入（不带大括号）
2. 一个文件里，有且只能有一个export default。但可以有多个export。
3. 当用export name 时，就用import { name }导入（记得带上大括号）
4. 当一个文件里，既有一个export default people, 又有多个export name 或者 export age时，导入就用 import people, { name, age }
5. 当一个文件里出现n多个 export 导出很多模块，导入时除了一个一个导入，也可以用import * as example
### **一个简单的闭包，以及对闭包的理解**
- 内部函数---即函数定义和函数表达式位于另一个函数的函数体内。内部函数在包含它们的外部函数之外被调用时，就会形成闭包。
```
function init() {
    var name = "Mozilla"; // name 是一个被 init 创建的局部变量
    function displayName() { // displayName() 是内部函数,一个闭包
        alert(name); // 使用了父函数中声明的变量
    }
    displayName();
}
init();
```
### **用css实现垂直左右居中(两种)**
- html：
```
<div class="box box1">
    <span>垂直居中</span>
</div>
```
- css：
1. table-cell
```
.box {
display: table-cell;
vertical-align: middle;
text-align: center;}
```
2. display:flex
```
.box {
    display: flex;
    justify-content:center;
    align-items:Center;
}
```
3. display:flex和margin:auto
```
.box{
    display: flex;
    text-align: center;
}
.box span{
    margin: auto;
}
```
4. translate
```
.box {
    position: absolute;
    top:50%;
    left:50%;
    width:100%;
    transform:translate(-50%,-50%);
    text-align: center;
}
```
5. 绝对定位和0
```
.box{
    width: 50%;
    height: 50%;
    background: #000;
    overflow: auto;
    margin: auto;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
}
```
6. 绝对定位和负边距
```
.box{
    position:relative;
}
.box span{ 
    position: absolute;
    width:100px;
    height: 50px;
    top:50%;
    left:50%;
    margin-left:-50px;
    margin-top:-25px;
    text-align: center;
}
```
### **用JavaScript解析以下URL中的参数, 并生成一个{a : b , c : d}格式的对象。**
```
function getQueryObject(url) {
    url = url == null ? window.location.href : url;
    var search = url.substring(url.lastIndexOf("?") + 1);
    var obj = {};
    var reg = /([^?&=]+)=([^?&=]*)/g;
    search.replace(reg, function (rs, $1, $2) {
        var name = decodeURIComponent($1);
        var val = decodeURIComponent($2);
        val = String(val);
        obj[name] = val;
        return rs;
    });
    return obj;
}
```
### **用js实现千位分隔符（正则+replace）**
```
function commafy(num) {
    num = num + '';
    var reg = /(-?d+)(d{3})/;
    if(reg.test(num)){
        num = num.replace(reg, '$1,$2');
    }
    return num;
}
```