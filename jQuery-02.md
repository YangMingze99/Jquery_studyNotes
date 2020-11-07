## **jQuery** **属性操作**

### **设置或获取元素固有属性值** **prop()**

所谓元素固有属性就是元素本身自带的属性，比如 <a>元素里面的 href ，比如 <input>元素里面的 type。

**获取语法：**

> prop(''属性'')
>

**设置属性语法**

> prop(''属性'', ''属性值'')

```
change事件，表单中checked属性
```

### **设置或获取元素自定义属性值** **attr()**

```
用户自己给元素添加的属性，我们称为自定义属性。比如给 div 添加 index=“1”。 
```

**获取属性语法**

attr(''属性'')      // 类似原生 getAttribute()

**设置属性语法**

attr(''属性'', ''属性值'')   //类似原生 setAttribute()

### **数据缓存** **data()**【了解】

当做变量存储

```
data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构，所以元素上无法查看。一旦页面刷新，之前存放的数据都将被移除。
```

 **附加数据语法**

data(''name'',''value'')   // 向被选元素附加数据   

**获取数据语法**

date(''name'')             //   向被选元素获取数据   

**例如：**

```javascript
$('span').data('spanindex',3);

console.log($('span').data('spanindex'));
```

### 购物车案例：

#### 案例：购物车案例**模块-全选**

```
①全选思路：里面3个小的复选框按钮（j-checkbox）选中状态（checked）跟着全选按钮（checkall）走。

②因为checked 是复选框的固有属性，此时我们需要利用prop()方法获取和设置该属性。

③把全选按钮状态赋值给3小复选框就可以了。

④当我们每次点击小的复选框按钮，就来判断：

⑤如果小复选框被选中的个数等于3 就应该把全选按钮选上，否则全选按钮不选。

⑥:checked 选择器      :checked 查找被选中的表单元素。

change改变到时候，获取当前input的checked状态，赋值给小按钮和全选按钮既可

小按钮改变的时候，判断选中个数和总个数，修改大按钮是否要选中
```

## **jQuery** **内容文本值**

**普通元素内容** **html()****（相当于原生inner HTML)

​	获取：html()   // 获取元素的内容

​	设置：html(''内容'')   // 设置元素的内容

**普通元素文本内容** text()   (相当与原生innerText)

​	获取：text()   // 获取元素的文本内容

​	设置：text(''文本内容'')   // 设置元素的文本内容

**表单的值** **val()**（ 相当于原生****value)

​	获取：val()   // 获取表单的值

​	设置：val(''内容'')  // 设置表单的值

#### **案例：购物车案例**模块**-**增减商品数量

```
①核心思路：首先声明一个变量，当我们点击+号（increment），就让这个值++，然后赋值给文本框。

②注意1： 只能增加本商品的数量， 就是当前+号的兄弟文本框（itxt）的值。 

③修改表单的值是val() 方法

④注意2： 这个变量初始值应该是这个文本框的值，在这个值的基础上++。要获取表单的值

⑤减号（decrement）思路同理，但是如果文本框的值是1，就不能再减了，直接return false即可
```

#### 购物车案例模块-修改商品小计

```
①核心思路：每次点击+号或者-号，根据文本框的值 乘以 当前商品的价格  就是 商品的小计

②注意1： 只能增加本商品的小计， 就是当前商品的小计模块（p-sum）  

③修改普通元素的内容是text() 方法

④注意2： 当前商品的价格，要把￥符号去掉再相乘 截取字符串 substr(1)

⑤parents(‘选择器’) 可以返回指定祖先元素  

⑥最后计算的结果如果想要保留2位小数 通过 toFixed(2)  方法

⑦用户也可以直接修改表单里面的值，同样要计算小计。 用表单change事件

⑧用最新的表单内的值 乘以 单价即可  但是还是当前商品小计

点击获取单价和数量相乘的结果保存给小计既可
用户直接输入数字问题
```

parents获取祖先元素方法

## **jQuery** **元素操作**

> 主要是遍历、创建、添加、删除元素操作。
>

**遍历元素**

jQuery 隐式迭代是对同一类元素做了同样的操作。如果想要给同一类元素做不同操作，就需要用到遍历。

> 语法1：$("div").each(function(index, domEle) { xxx; }）

```
1. each() 方法遍历匹配的每一个元素。主要用DOM处理。 each 每一个

2. 里面的回调函数有2个参数：  index 是每个元素的索引号;  demEle 是每个DOM元素对象，不是jquery对象

3. 所以要想使用jquery方法，需要给这个dom元素转换为jquery对象  $(domEle)
```

语法2：$.each(object，function(index, element){ xxx;}）

```
1. $.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象

2. 里面的函数有2个参数：  index 是每个元素的索引号;  element  遍历内容
```

*案例：购物车案例 * 模块-计算总计和总额

```
①核心思路：把所有文本框里面的值相加就是总计数量。总额同理

②文本框里面的值不相同，如果想要相加需要用到each遍历。声明一个变量，相加即可

③点击+号-号，会改变总计和总额，如果用户修改了文本框里面的值同样会改变总计和总额

④因此可以封装一个函数求总计和总额的， 以上2个操作调用这个函数即可。

⑤注意1： 总计是文本框里面的值相加用 val()     总额是普通元素的内容用text()  

⑥要注意普通元素里面的内容要去掉￥并且转换为数字型才能相加

多次需要求总计，所有封装函数最为合适
```

**创建元素**

> 语法：$(''<li></li>'');    
>

**添加元素**

> element.append(''内容'') [把内容放入匹配元素内部最后面，类似原生 appendChild。]
>
> element.prepend(''内容'') 把内容放入匹配元素内部最前面。

**外部添加**

> element.after(''内容'') // 把内容放入目标元素后面
>
> element.before(''内容'')    //  把内容放入目标元素前面 
>

```
①内部添加元素，生成之后，它们是父子关系。

②外部添加元素，生成之后，他们是兄弟关系。
```

**删除元素**

> element.remove()   //  删除匹配的元素（本身）
>
> element.empty()    //  删除匹配的元素集合中所有的子节点
>
> element.html('''')   //  清空匹配的元素内容
>

```
①remove 删除元素本身。

②empt() 和  html('''') 作用等价，都可以删除元素里面的内容，只不过 html 还可以设置内容。
```

**案例：购物车案例模块-删除商品模块**

```
①核心思路：把商品remove() 删除元素即可

②有三个地方需要删除： 1. 商品后面的删除按钮 2. 删除选中的商品 3. 清理购物车

③商品后面的删除按钮： 一定是删除当前的商品，所以从 $(this) 出发

④删除选中的商品： 先判断小的复选框按钮是否选中状态，如果是选中，则删除对应的商品

⑤清理购物车： 则是把所有的商品全部删掉
```

**案例：购物车案例模块-选中商品添加背景**

```
①核心思路：选中的商品添加背景，不选中移除背景即可

②全选按钮点击：如果全选是选中的，则所有的商品添加背景，否则移除背景

③小的复选框点击： 如果是选中状态，则当前商品添加背景，否则移除背景

④这个背景，可以通过类名修改，添加类和删除类
```

## **jQuery** **尺寸、位置操作**

### **jQuery 尺寸**

> width()、height()【只算width和height】
>
> innerWidth()、innerHeight()【包含padding+width】
>
> outerWidth()、outerHeight()【包含padding、border、width】
>
> outerWidth(true)、outerHeight(true)【包含padding、border、margin、width】

```
以上参数为空，则是获取相应值，返回的是数字型。
如果参数为数字，则是修改相应值。
参数可以不必写单位。
```

### **jQuery 位置**

> 位置主要有三个： offset()、position()、scrollTop()/scrollLeft();

**offset()设置或获取元素偏移**
offset：距离文档的距离【left，top】

```
①offset() 方法设置或返回被选元素相对于**文档**的偏移坐标，跟父级没有关系。

②该方法有2个属性 left、top 。offset().top  用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离。

③可以设置元素的偏移：offset({ top: 10, left: 30 });
```

**position()** 获取元素偏移

①position() 方法用于返回被选元素相对于**带有定位的父级**偏移坐标，如果父级都没有定位，则以文档为准。

②该方法有2个属性 left、top。position().top 用于获取距离定位父级顶部的距离，position().left 用于获取距离定位父级左侧的距离。

注意：该方法只能获取。

**scrollTop()、scrollLeft()设置**或获取元素被卷去的头部和左侧

①scrollTop() 方法设置或返回被选元素被卷去的头部。

②不跟参数是获取，参数为不带单位的数字则是设置被卷去的头部。

scroll事件

#### **案例带有动画的返回顶部**

```
①核心原理： 使用animate动画返回顶部。

②animate动画函数里面有个scrollTop 属性，可以设置位置

③但是是元素做动画，因此 $(“body,html”).animate({scrollTop: 0})
```

#### **案例：电梯导航**

```
①当我们滚动到 今日推荐 模块，就让电梯导航显示出来

②点击电梯导航页面可以滚动到相应内容区域

③核心算法：因为电梯导航模块和内容区模块一一对应的

④当我们点击电梯导航某个小模块，就可以拿到当前小模块的索引号

⑤就可以把animate要移动的距离求出来：当前索引号内容区模块它的offset().top

⑥然后执行动画即可
```

```
第二部分：

①当我们点击电梯导航某个小li， 当前小li 添加current类，兄弟移除类名

②当我们页面滚动到内容区域某个模块， 左侧电梯导航，相对应的小li模块，也会添加current类， 兄弟移除current类。

③触发的事件是页面滚动，因此这个功能要写到页面滚动事件里面。

④需要用到each，遍历内容区域大模块。 each里面能拿到内容区域每一个模块元素和索引号

⑤判断的条件：  被卷去的头部 大于等于 内容区域里面每个模块的offset().top

⑥就利用这个索引号找到相应的电梯导航小li添加类。       
```