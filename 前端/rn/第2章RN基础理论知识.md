### 2-1 环境搭建

1.  安装node.js
1.  安装watchman，用于rn文件监听

### 2-2 项目调试

1.  Developer Menu开发者菜单，在移动设备上打开
2.  Chrome开发者工具，在开发者菜单中可以打开chrome开发者工具

### 2-3 ES6标准

1.  ES是一种标准化语言
2.  ES6特性
    1. 类
    2. 模块化
        模块可以通过export规定对外暴露的接口，通过import引用其他模块提供的接口，export可以导出多个变量常量或函数。

        ```javascript
        // 导入函数和变量
        import {myModule} from 'myModule' import {name, age} from 'test'
    4.  箭头函数
        箭头函数之前是空括号、单个参数名、多个参数名，箭头后是一个表达式（作为函数的返回值），或者是用花括号括起的函数体（需要自行通过return来返回，否则返回的是undefined）
        
        ```javascript
        var sum = x => x + 2
        
        //如果参数不是一个，需要用()括起来
        var sum = (x, y) => x + y
        sum(6, 2);  //8
        
        //当箭头函数有多行语句，用{}包裹起来，表示代码块，只有一行时可以省略{}
        var f = (a, b) => {
        	let result = a + b 
        	return result
        }
        
        //当箭头函数需要返回对象的时候，为了区分代码块，要用()括起来
        var f = (id, name) => ({id: id, name: name})
        f(6, 2) // {id: 6, name: 2}
        ```
    5.  函数参数默认值
        
        ```js
        function foo(height = 50, color = 'red'){
        	//...
        }
        ```
    6.  模板字符串
        使用\${}完成字符串拼接，将变量放在大括号中。
        
        ```js
        // 不使用模版字符串
        var name = 'Your name is ' + first + ' ' + last + '.'
        // 使用模版字符串
        var name = 'Your name is `${first} $`{last}.'
        ```
    7.  解构赋值
        1.  获取数组中的值
            
            ```js
            var foo = ['one', 'two', 'three', 'four']
            var [one, two, three] = foo
            console.log(one) // 'one'
            console.log(two) // 'two'
            
            // 如果你要忽略某些值，你可以按照下面的写法获取你想要的值
            var [first, , , last] = foo;
            console.log(first) // 'one'
            console.log(last) // 'four'
            
            // 你也可以这样写
            var a, b // 先声明变量
            [a, b] = [1, 2];
            console.log(a) // 1
            console.log(b) // 2
            
            // 如果没有从数组中获取到值，你可以为变量设置一个默认值
            var a, b;
            [a = 5, b = 7] = [1]
            console.log(a) // 1
            console.log(b) // 7
            
            //通过解构赋值可以方便的交换两个变量的值
            var a = 1;
            var b = 3;
            [a, b] = [b, a];
            ```
        2.  获取对象中的值
            
            ```js
            const student = {
              name: 'Ming',
              age: '18',
              city: 'Shanghai'
            }
            const {name, age, city} = student
            console.log(name) // 'Ming'
            ```
    8.  延展操作符
        1.  延展操作符
            ...可以在函数调用/数组构造时，将数组表达式或者string在语法层面展开；还可以在构造对象时，将对象表达式按key-value的方式展开。
            
            ```js
            // 函数调用，对象的每一个属性作为函数入参数
            myFunction(...iterableObj)
            // 展开字符串
            [...iterableObj, '4', ...'hello', 6]
            let objClone = {...obj}
            ```
        2.  使用场景
            1.  在函数调用时使用延展操作符
                ```js
                function sum(x, y, z) {
                	return x + y + z
                }
                const numbers = [1, 2, 3]
                // 不使用延展操作符
                console.log(sum.apply(null, numbers))
                // 使用延展操作符
                console.log(sum(...numbers))
                ```
            2.  构造数组
                没有展开语法的时候，只能组合使用push，splice，concat等方法，来将已有数组元素变成新数组的一部分，有了展开语法，构造新数组会变得更简单、更优雅。
                
                ```js
                const students = ['Jine', 'Tom']
                const persons = ['Tony', ...students, 'Aaron', 'Anna']
                
                // 数组拷贝
                var arr = [1, 2, 3]
                var arr2 = [...arr]
                arr2.push(4)
                
                // 连接多个数组
                var arr1 = [0, 1, 2]
                var arr2 = [3, 4, 5]
                var arr3 = [...arr1, ...arr2]
                // 等价于
                var arr3 = arr1.concat(arr2)
                ```
            3.  对对象的支持
                
                ```js
                var obj1 = {foo: 'bar', x: 42}
                var obj2 = {foo: 'baz', y: 13}
                var cloneObj = {...obj1}
                // 克隆后的对象：{foo: 'bar', x: 42}
                
                var cloneObj = {..obj1, ...obj2}
                // 合并后的对象：{foo: 'baz', x: 42, y: 13}
                ```
            4.  在react中的应用
                通常我们封装一个组件时，会对外公开一些props用于实现功能。大部分情况下在外部使用都应显式地传递props。但是当传递大量props时，会非常繁琐，这时我们可以使用延展操作符（用于取出对象的所有可遍历属性）来进行传递
                
                ```js
                // 一版情况下我们这样写： 
                <CustomComponent name = 'Jine' age = {21} />
                // 使用...，等同于上面的写法
                const params = {
                  name: 'Jine',
                  age: 21
                }
                <CustomComponent {...params} />
                ```
                
                
            5.  配合解构赋值避免传入不需要的参数
    9.  对象属性简写
        在ES6中允许我们在设置一个对象的属性时可以不指定属性名，只需对象属性名与将要赋值的常量名相同即可。
        
        ```js
        // 不使用ES6，对象中必须包含属性和值，显得非常冗余
        const name='Ming', age='18', city='Shanghai'
          const student = {
          name: name,
          age: age,
          city: city
        }
        // 使用ES6
        const name='Ming', age='18', city='Shanghai'
        const student = {
          name,
          age,
          city
        }
        ```
    10. Promise
        异步编程，替换callback
        
        ```js
        // 嵌套两个setTimeout回调函数：
        // 不使用ES6
        setTimeout(function() {
        	console.log('Hello') // 1秒后输出'Hello'
          setTimeout(function() {
          	console.log('Hi') // 2秒后输出“Hi”
          }, 1000)
        }, 1000)
        
        // 使用ES6
        var waitSecond = new Promise(function(resolve, reject) {
            setTimeout(resolve, 1000)
        })
        waitSecond.then(function() {
            console.log('Hello')
            // 这里个人猜测是第一次调用then后then中代码块中的返回值作为			// 链式调用的返回值，因此必须返回waitSecond，才能二次调用			// then
            return waitSecond
        }).then(function(){
            console.log('Hi')
        })
        ```
    11. 支持let与const
        在之前js是没有块级作用域的，const与let填补了这方面的空白，const与let都是块级作用域。
        
        ```js
        // 使用var定义的变量为函数级作用域
        {
        	var a = 10
        }
        console.log(a) //输出10
        // 使用let与const定义的变量为块级作用域
        {
           let a = 10
        }
        console.log(a) //报错
        ```
3.  ES7特性
    1.  includes函数
        用来判断一个数组是否包含指定的值，与indexOf函数很相似
        
        ```js
        // 以下两个表达式是等价的：
        arr.incudes(x)
        arr.indexOf(x) >= 0
        ```
        
        
    2.  指数操作符
4.  ES8特性
    1.  async和await
        也就是我们所说的异步函数，async/await将我们从头痛的回调地狱中彻底解脱出来了，使整个代码看起来很简洁。

### 2-4 React基础

1.  声明式渲染和命令式渲染\
    传统的命令式编程，是告诉机器怎么去做事情，而声明式编程是告诉机器你想要做什么，至于怎么做让机器自己实现。
2.  如何使用\
    如果构建一个react的单页应用，可以通过create-react-app这个脚手架工具完成，开发rn则不行。
3.  JSX语法\
    JSX是一种xml的语法扩展，每一个xml标签都会被JSX转换成纯js代码。
4.  js表达式
    1.  属性表达式\
        要使用属性表达式，只需要将这个表达式用一对大括号包起来。
        var person = \<Person name={window\.isLoggedIn ? window\.name : ''}>
    2.  子节点表达式\
        以上的方式同样可以用于描述子节点
        var content = \<Container>{window\.isLoggedIn ? <nav /> : \<Login  />}\</Container>
    3.  注释\
        JSX的注释，也是一种表达式
    4.  不推荐直接修改组件的属性
        var component = \<Component />;
        component.props.foo = x;
        component.props.bar = y;
        以上做法是不推荐的，因为这样修改React不会对组件的属性类型进行检查，从而引发问题。推荐做法：
        var component = \<Component foo={x} bar={y}/>
    5.  延展属性
    6.  Component\
        React允许将代码封装成组件，然后像普通HTML标签一样，在网页中插入。
        //React中所有组件都继承React.Component
        class Hello extends React.Component {
        render() {
        return <h1>Hello {this.props.name}</h1>;
        }
        }
        ReactDOM.render( \<Hello name="John" />,
        document.getElementById('example')
        )
        上面代码中，Hello就是一个组件类，模版插入\<Hello />时，会自动生成一个Hello的实例，所以组件类都必须有render方法，用于输出组件。
    7.  遍历组件对象属性\
        this.props.children会返回组件对象的所有属性。React提供一个工具方法React.Children来处理this.props.children。可以用React.Children.map或React.Children.forEach来遍历子节点。
    8.  PropTypes
        组件属性可以接受任意值，所以需要一种机制来验证参数是否符合要求。组件类的PropTypes属性就是这个作用。
        import PropTypes from 'prop-types'
        class MyTitle extends React.Component {
        static propTypes={
        title\:PropTypes.string.isRequired,
        };
        render(){
        return <h1>title:{this.props.title}</h1>;
        }
        }
        上述代码中，PropTypes告诉React，这个title属性是必须的，而且它的值必须是字符串，如果使用时不传或者传入其他类型，程序就会报错。
    9.  默认属性\
        defaultProps可以用来设置组件属性的默认值。
        class MyTitle extends React.Component{
        static defaultProps={
        shortName:'MyTitle'
        };
        render(){
        return <h1>{this.prpos.shortName}</h1>;
        }
        }
    10. ref属性\
        组件不是真实的DOM节点，而是虚拟DOM，当它插入到文档后才变成真实的DOM，React规定所有的DOM变动都先在虚拟DOM上，然后再根据发生变动的部分反映在真实DOM上，提高性能，ref用于获取真实的DOM节点
    11. state\
        this.props和this.state都用于描述组件的特性，this.props表示那些组件无法改变的特性，而this.state表示随着用户交互而产生变化的属性。
    12. react组件的生命周期\
        mounting状态，初始化时会调用构造方法和render进行渲染，渲染完成后更新到真实DOW
    13. render()\
        render()方法返回null或布尔值，就不会渲染
    14. componentDidMount()\
        这个生命周期方法在组件被装载后会立即被调用，通常可以在这个方法中做一些初始化的操作，与构造方法的区别是，componentDidMount方法可以获取到真实DOM节点，而构造方法中是获取不到的。
    15. shouldComponentUpdate()\
        当组件接收到新的props或者state，将在render之前，调用这个生命周期方法，返回一个布尔值，告诉React是否需要重新渲染。
    16. getSnapshotBeforeUpdate()\
        不常用。
    17. componentDiDUpdate()\
        组件的更新已经同步到DOM之后会回调这个方法。
    18. componentWillUnmount()\
        组件从DOM中移除时会回调这个方法，在这个方法中通常进行定时器或监听器的移除等操作。

### 2-5 rn布局知识

1.  宽高尺寸像素无关\
    rn中的尺寸是没有单位的，代表了设备独立像素。
    \<View style={{width:100, height:100,margin:40,backgroundColor:'gray'}}> \<Text style={{fontSize:16,margin:20}}>尺寸\</Text> \</View>
    上述代码，运行在Android上时，View的长宽被解析为100dp，字体被解析为16sp，运行在ios上时尺寸被解析为pt，这样就确保了布局在不同dpi的手机屏幕上显示不会发生改变。
2.  rn中的FlexBox和css3的FlexBox工作方式是一样的，但是有些地方还是有出入的。
3.  rn支持的Flex属性
    1.  主轴和侧轴\
        主轴是从左至右，侧轴是从上至下。
    2.  父视图属性(容器属性)
        1.  flexDirection\
            flexDirection属性定义了父试图中子元素沿横轴或侧轴的排列方式，相当于css的flex-direction。
            flexDirection:'row' //从左至右依次排列
            flexDirection:'row-reverse' //从右至左依次排列
            flexDirection:'column'  //从上向下排列，默认的排列方式
            flexDirection:'column-reverse'  //从下向上排列
        2.  flexWrap\
            flexWrap属性定义了子元素在父视图内是否允许多行排队，即一行显示不下时是否能换行显示，默认为nowrap，相当于css的flex-wrap。
        3.  justifyContent\
            justifyContent属性定义了子元素的空间分配方式，相当于css中的justify-content。
            justifyContent:'flex-start' //从行头紧挨着填充，默认值
            justifyContent;'flex-end'   //从行尾紧挨着填充
            justifyContent:'center' //居中填充，如果剩余空间是负的，则子元素将在两个方向上同时溢出
            justifyContent:'space-between'  //在每行上均匀分配，相邻元素间隔相同，第一个元素与行首对齐，最后一个元素与行尾对齐
            justifyContent:'space-around'   //在每行上均匀分配，相邻元素间隔相同，第一个元素到行首的距离和最后一个元素到行尾的距离是相邻元素距离的一半
        4.  alignItems\
            alignItems属性可以决定其子元素沿着次轴（与主轴垂直的轴，比如若主轴方向为row，则次轴方向为column）的排列方式。
            alignItems:'flex-start' //元素向次轴起点对齐
            alignItems:'flex-end'   //元素向次轴终点对齐
            alignItems:'center' //元素在次轴居中
            alignItems:'strech' //元素拉伸，在次轴上填满，当次轴为纵轴时，如果限制了元素高度则不会拉伸；当次轴为横轴时，如果限制了元素高度则不会拉伸
    3.  子视图属性
        1.  alignSelf\
            alignSelf属性定义了子视图的对齐方式，注意，alignSelf属性可重写父视图的alignItems属性。
            alignSelf:'auto'    //默认属性，继承父识图的alignItems属性
            alignSelf:'stretch'  //元素被拉伸以适应容器，与alignItems一样，限制了高度和宽度就会不生效
        2.  flex\
            即权重，默认是0，Android中的weight
    4.  其他属性\
        borderColor、borderWidth，margin外边距，padding内边距(占用自身尺寸)

### 2-6 高性能列表组件

1.  ListView卡顿占内存，因为ListView中的item是全量渲染的，没有复用机制。
2.  VirtualizedList\
    VirtualizedList是FlatList和SectionList的底层实现，具体屏幕显示区域越近的item渲染优先级越高，反之越低，太远了则不渲染。
3.  VirtualizedList注意事项
    1.  当item滑出显示区域后，其内部状态不会保留，要确保能保留数据;
    2.  本组件继承自PureComponent而非Component，PureComponent是优化React程序的重要方法，可以减少不必要的render操作次数，从而提高性能，原理是在PureComponent内部的shouldComponentUpdate里，对props/state做了一个浅对比，如果没有发生改变，就不会触发render方法。浅比较只比较两个对象的内存地址是否相同，深比较是递归对比两个对象的所有属性是否相同。这意味着要检察renderItem函数所依赖的props数据，如果是一个引用类型，则需要先修改其内存地址，再修改值，否则不会刷新。
    3.  如果用户滑动速度超过渲染速度，则有可能看到空白。
4.  FlatList属性
    1.  data：数据源，目前只接收数组
    2.  renderItem：每一行渲染的布局
    3.  onReresh：刷新回调
    4.  refreshControl={}：下拉刷新
    5.  RefreshControl: 自定义loading样式
    6.  ListFooterComponent：上拉加载
    7.  data.item：代表每一个item数据
5.  SectionList属性
    1.  sections：数据源
    2.  section.section：代表一组数据
    3.  renderSectionHeader：渲染分组头部
        以下两个函数相同，第二个代表从data中取出section
        \_renderSectionHeader(data) {
        return \<View> \<Text>{data.section.title}\</Text> \</View>
        }
        \_renderSectionHeader({section}) {
        return \<View> \<Text>{section.title}\</Text> \</View>
        }
    4.  ItemSeparatorComponent：分割线