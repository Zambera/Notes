# VUE--渐进式 JS 框架

> 动态构建显示用户界面

- 遵循MVVM模式

- 编码简介，体积小，运行效率高，适合移动 / PC端开发

- 本身只关注UI，便于引入vue插件或其他第三方库

  ​	＊　借鉴angular的**模板**和**数据绑定**技术

  ​	＊　借鉴react的**组件化**和**虚拟DOM技术**

#### Vue扩展插件

1. vue-cli：脚手架
2. vue-resource(axios)： ajax请求   不用
3. vue-router：路由
4. vuex：状态管理
5. vue-lazyload：图片懒加载
6. vue-scroller：页面滑动相关
7. mint-ui：基于vue的UI组件库（移动端）
8. element-ui ：基于vue的UI组件库（PC端）

### 模板语法

~~~~js
1. 插值语法 {{表达式}} //从模板绑定数据
2.指令 ：强制数据绑定
<a v-bind:href='url'></a>
<a :href='url'></a>
3.指令 ：绑定事件监听
<button v-on:click:'test'></botton> //v-on:事件='方法'
<button @click='test'></botton>    

new Vue({
    el:'#app',
    data:
})
~~~~

#### Object.defineProperty(obj,prop,descriptor)

函数对象的方法 在函数上定义一个新的属性，或者修改一个对象的现有属性

~~~~js
obj
const p={
    firstName:"A",
    lastName:'B'
}
/**
	给p添加新的属性 fullName=firstName+'-'+lastName
	修改firstName或lastName fullName随之改变
	修改fullName firstName或lastName随之改变
*/
1.不满足
p.fullName=p.firstName+'-'+lastName
2.
Object.defineProperty(p,'fullName',{//配置对下个
    get(){//是回调函数
        //读取属性值时，自动调用，将函数 的返回值作为属性值，this指函数所在的对象
        return this.firstName+'-'+lastName
    },//  getter
    set(value){
        //value是 fullName 修改后的值
        //当修改了属性值时调用，监视属性值变化，this指函数所在的对象
        const names=value.split('-')
        this.firstName=names[0]
        this.lastName=names[1]       
    }//  setter
})
~~~~

#### 计算属性、计算属性缓存

~~~~js
/*
通过getter和setter实现对属性数据的显示和监视
计算属性存在缓存，多次读取只执行一次getter
{
	计算属性名(字符串)：计算属性值(任意类型)
}
*/
computed: {
    fullName1() {
        console.log('fullName1()')
        return this.firstName + '-' + this.lastName
    },
    fullName3: {
        get() {
            console.log('fullName1 get()')
            return this.firstName + '-' + this.lastName
        },
        set(value) {
            console.log('fullName1 set()')
            const names = value.split('-')
            this.firstName = names[0]
            this.lastName = names[1]
        }
    },
},
~~~~

#### class和style的绑定

~~~~js
//样式变化
//		class
//类名不确定,静态类名一定有
<p class='classC' :class='myClass'></p>
//对象形式 类名确定，不确定有无
<p :class='{classA:true,classB:false}'></p>
<p :class='{classA:hasA,classB:hasB}'></p>
//数组形式 不常用
<p :class='[classA,classB]'></p>

//		style
<p :style='{color:activeColor,fontSize:fontSize}'>
~~~~

#### 根据条件进行渲染

~~~~js
//通过v-if 隐藏  标签被删除
<p v-if="ok">表白成功</p>
<p v-else>表白失败</p>
//通过 v-show 隐藏 是通过display:none隐藏
~~~~

### 遍历数组和对象

~~~~Js
//遍历数组
<ul>
    <li v-for="(p, index) in persons" :key="p.id">
        {{p.id}}---{{p.name}}----{{p.age}} --
        <button @click='deleteP(index)'>删除</button> --
        <button @click='updateP(index,{id:Date.now(),name:"cat",age:17})'>更新</button>
    </li>
</ul>
new Vue({
    el: '#demo',
    data: {
        persons: [{
            id: 1,
            name: 'Tom',
            age: 15
        }, {
            id: 2,
            name: 'Mike',
            age: 19
        }, {
            id: 3,
            name: 'Jack',
            age: 18
        }, {
            id: 4,
            name: 'Amber',
            age: 20
        }, ]
    },
    methods: {
        deleteP(index) { //不能写delete
            this.persons.splice(index, 1)
        },
        updateP(index, newP) {
            this.persons.splice(index, 1, newP) //替换，vue重写过
            //this.persons[index] = newP //不可行，数据绑定失效
            this.persons[index].id=newP.id	//可行
        }
    },
})
/*	数组元素变化检测
vue中内部如何监视数据的变化
1.对象中的属性数据(响应式属性：当修改元素时，内部自动更新对应的界面)
	给属性添加setter方法
2.数组中的元素数据
	重写(重新定义)数组的一系列更新数组的方法
	1).调用原生数组对应的方法，对数组元素进行处理
	2).更新界面
*/
~~~~

#### 过滤和排序

~~~~js
computed: {
    //过滤后的新数组
    filterPersons() {
        //1.取出依赖数据
        const {
            searchName,
            persons,
            sortType,
        } = this
        //2.计算产生新数据
        const arr = persons.filter((p, index) => {
            //过滤函数 返回布尔值
            return p.name.indexOf(searchName) !== -1
        })

        //可能排序（升/降）
        if (sortType !== 1) {
            arr.sort((p1, p2) => {
                if (sortType === 3) {
                    return p2.age - p1.age
                } else {
                    //如果返回值大于0，将p2放在左边-升序
                    return p1.age - p2.age
                }
            })
        }
        //3.返回新数组
        return arr
    }
}
~~~~

#### 事件处理

~~~~js
//1.绑定监听
<button v-on:click="test1"></button>
<button @click="test1(name,$event)"></button>

//2.事件修饰符
//阻止默认事件
<a @click.prevent='test4'></a>
//阻止事件冒泡
@click.stop='test'//绑定在内部
//
@click.once//一次事件
//按键修饰符，功能键
keyup.13||keyup.enter

~~~~

#### 表单数据收集

~~~~html
<div id="demo">
    <form action="xxx">
        <span>用户名：</span>
        <input type="text" v-model="user.username"><br>

        <span>密码:</span>
        <input type="password" v-model="user.pwd"><br>

        <span>性别：</span>
        <input type="radio" id="female" v-model="user.sex" value="female">
        <label for="female">女</label>
        <input type="radio" id="male" v-model="user.sex" value="male">
        <label for="male">男</label><br>

        <span>爱好：</span>
        <input type="checkbox" id="basket" v-model="user.likes" value="basket">
        <label for="basket">篮球</label>
        <input type="checkbox" id="foot" v-model="user.likes" value="foot">
        <label for="foot">足球</label>
        <input type="checkbox" id="pingpang" v-model="user.likes" value="pingpang">
        <label for="pingpang">乒乓球</label><br>

        <span>城市：</span>
        <select name="" id="" v-model="user.cityID">
          <option value="">未选择</option>
          <option :value="city.id" v-for="city in user.allCitys" :key="city.id">{{city.name}}</option>
      </select><br>

        <textarea v-model="user.info" name="" id="" cols="30" rows="10"></textarea>
        <br>
        <input type="submit" value="注册" @click.prevent='register'>
    </form>
</div>
~~~~

~~~~js
new Vue({
el: '#demo',
data() {
    return {
        user: {
            username: '',
            pwd: '',
            sex: 'male',
            likes: ['foot'],
            allCitys: [{
                id: 1,
                name: 'BJ'
            }, {
                id: 2,
                name: 'SH'
            }, {
                id: 3,
                name: 'SZ'
            }, ],
            cityID: 3,
            info: '',
        }

    }
},
methods: {
    register() {
        const user = {}
        alert('提交注册的ajax请求' + JSON.stringify(this.user))
    }
},
})
~~~~



VUE全局配置

VUE全局API－－函数对象的一些方法

VUE实例vm.$