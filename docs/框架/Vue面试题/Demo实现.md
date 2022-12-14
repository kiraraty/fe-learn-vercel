---
sidebar_position: 11
description: Demo
---

## Demo 实现

### 模板

组件化

```js
<template>
	<div>
    </div>
</template>
<script>
import
export default{
    data(){
        return {

        }
    },
     computed:{

     },
     watch:{

     },
     methods:{

    }
}
</script>
<style lang="less" scoped>

</style>
```

html

```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <div id="app">
        姓： <input type="text" v-model=firstName> 名：
        <input type="text" v-model=lastName> 姓名：
        <span>{{fullname}}</span>
    </div>
 </body>
<script type="text/javascript">
    var app = new Vue({
        el: "#app",
        data: {
            firstName: 'z',
            lastName: 's'
        },
        computed: {
            fullname() {
                return this.firstName + this.lastName
            }
        },
        watch: {
            firstName(newval) {
​
                this.fullname = newval + this.lastName
            },
            lastName(newval) {
                this.fullname = this.firstName + newval
            }
​
        },
        methods:{

    }
    })
​
</script>
</html>
```

vue3

```js
<script lang="ts">
export default defineComponent({
  components:{
  props: {
      number:{
          type:Number,
          default:0
      }
  },
  emit:[],
  setup(props,context){
      const countRef=ref(null)
      watch(
          ()=>props.number,
          ()=>update(props.number)
      )
      onMounted(()=>{
          func()
      })
      const func()=>{




      }
      return count
  }
  })
</script>
<style>
<style>

```

vue3.2

```js
<template>
	<div>
    </div>
</template>
<script lang="ts" setup>
import
</script>
<style>
</style>
```

### 1.实现一个 modal 框

```js
<template>
  <div class="container">
    <transition name="modal-fade">
      <div class="modal-container" v-show="visible" :style="{ width: width }">
        <!-- 头部标题 -->
        <div class="modal-header">
          <div class="modal-title">{{ title }}</div>
          <i class="iconfont close-icon" @click="close">&#xe7fc;</i>
        </div>
        <!-- 内容区域 -->
        <div class="modal-content">
          <slot></slot>
        </div>
        <!-- 底部按钮 -->
        <div class="modal-footer" v-show="showOperation">
          <div class="modal-btn">
            <button class="cancel" ref="cancelBtn" @click="close" @mousedown="cancelMouseDown" @mouseup="cancelMouseUp">取消</button>
            <button class="ok" @click="ok">确认</button>
          </div>
        </div>
      </div>
    </transition>
    <!-- 遮罩层 -->
    <div class="mask" v-show="visible" @click="close"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  props: {
    // 模态框标题
    title: {
      type: String,
      default: () => {
        return '模态框标题'
      },
    },
    // 显示隐藏控件
    visible: {
      type: Boolean,
      default: () => {
        return false
      },
    },
    // 隐藏底部区域
    showOperation: {
      type: Boolean,
      dafault: () => {
        return true
      },
    },
    // 宽度
    width: {
      type: String,
      default: '250px',
    },
  },
  methods: {
    // 取消
    close() {
      this.$emit('cancel')
      this.$emit('update:visible', false)
    },
    // 确认
    ok() {
      this.$emit('submit')
      this.$emit('update:visible', false)
    },
    // 取消按钮 鼠标按下事件
    cancelMouseDown() {
      this.$refs.cancelBtn.style.color = '#096dd9'
      this.$refs.cancelBtn.style.border = '1px solid #096dd9'
    },
    // 取消按钮 鼠标松开事件
    cancelMouseUp() {
      this.$refs.cancelBtn.style.color = '#595959'
      this.$refs.cancelBtn.style.border = '1px solid #d9d9d9'
    },
  },
  watch: {
    // 操作遮罩层的展示/隐藏
    visible() {
      if (this.visible == true) {
        document.querySelector('body').setAttribute('style', 'overflow:hidden !important;')
      } else {
        document.querySelector('body').removeAttribute('style')
      }
    },
  },
}
</script>

<style scoped>
.modal-container {
  z-index: 999;
  background-color: #fff;
  min-width: 250px;
  min-height: 180px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border: none;
  border-radius: 4px;
  transition: 0.5s;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.modal-header {
  width: 100%;
  height: 50px;
  border: none;
  border-bottom: 1px solid #e8e8e8;
  padding: 20px 30px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.modal-title {
  color: #262626;
  font-weight: 600;
  font-size: 17px;
}
.close-icon {
  color: #4d4d4d;
  cursor: pointer;
  width: 80px;
  text-align: right;
}
.modal-content {
  width: 100%;
  min-height: 100px;
  border: none;
  border-radius: none;
  padding: 20px 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.modal-footer {
  width: 100%;
  height: 60px;
  border: none;
  border-top: 1px solid #e8e8e8;
  padding: 0 30px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.modal-btn {
  width: 150px;
  display: flex;
  justify-content: space-between;
}
.cancel {
  border: 1px solid #d9d9d9;
  background-color: #fff;
  color: #595959;
  width: 70px;
  height: 32px;
  border-radius: 4px;
  font-size: 14px;
  transition: 0.5s;
}
.cancel :hover {
  border: 1px solid #40a9ff;
  color: #40a9ff;
}
.ok {
  border: 1px solid #1890ff;
  background-color: #1890ff;
  color: #ffffff;
  width: 70px;
  height: 32px;
  border-radius: 4px;
  font-size: 14px;
  transition: 0.5s;
}
.ok :hover {
  border: 1px solid #40a9ff;
  background-color: #40a9ff;
}
.mask {
  z-index: 998;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
}
.modal-fade-enter-active {
  transition: all 0.3s ease;
}
.modal-fade-leave-active {
  transition: all 0.3s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  transform: translateX(-400px);
  opacity: 0;
}
</style>
```

### 2.实现一个 Confirm 框

```vue
<template>
  <div class="content-pop" v-if="bool_show">
    <div class="result" v-html="content"></div>
    <div class="bottom">
      <div class="cancel" @click="cancel">取消</div>
      <div class="confirm" @click="confirm">确定</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "msgConfirmPro",
  data() {
    return {
      bool_show: false,
      content: "",
      cancelBack: undefined,
      confirmBack: undefined,
    };
  },
  methods: {
    // 打开弹窗
    show(content, confirm, cancel) {
      if (confirm) {
        this.confirmBack = confirm;
      }
      if (cancel) {
        this.cancelBack = cancel;
      }
      this.content = content;
      this.bool_show = true;
    },
    cancel() {
      this.bool_show = false;
      if (this.cancelBack) {
        this.cancelBack();
      }
    },
    confirm() {
      this.bool_show = false;
      if (this.confirmBack) {
        this.confirmBack();
      }
    },
  },
};
</script>

<style scoped="">
.content-pop {
  width: 250px;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  /* padding: 0.04rem 0 0 0; */
  box-sizing: border-box;
  background: #ffffff;
  height: 149px;
  border-radius: 24px;
}

.result {
  overflow: auto;
  padding: 20px 30px;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  /* bottom: 87px; */
  font-size: 16px;
  position: absolute;
  text-align: center;
  color: #333;
  box-sizing: border-box;
  -webkit-overflow-scrolling: touch;
}
.content-pop .bottom {
  font-size: 16px;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  box-sizing: border-box;
  display: flex;
  justify-content: space-between;
  border-top: 1px solid #f5f5f5;
}

.content-pop .bottom .cancel {
  color: #666666;
  width: 50%;
  height: 100%;
  line-height: 48px;
  text-align: center;
  border-right: 01px solid #f5f5f5;
}

.content-pop .bottom .confirm {
  color: #2283e2;
  width: 50%;
  height: 100%;
  text-align: center;
  line-height: 48px;
}

.content-pop .title {
  box-sizing: border-box;
  padding: 40px 0;
  width: 100%;
  margin: 0 auto;
  text-align: center;
  color: #333;
  border-bottom: 0.003rem solid #f5f5f5;
}
</style>
```

使用

```vue
<template>
  <div id="app" style="background-color: #ff0000;height: 100vh;">
    <div @click="show()">点击出现弹窗</div>

    <ylConfirm ref="MSGCONFIRMPRO"></ylConfirm>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import ylConfirm from "./components/yl-confirm.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    ylConfirm,
  },
  methods: {
    show() {
      this.$refs.MSGCONFIRMPRO.show(
        "我是弹窗里面的内容，我可以随便定义哦",
        () => {
          // 确定的回调
          alert("点击了确认");
        },
        () => {
          // 取消的回调
          alert("点击了取消");
        }
      );
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

### 3.实现一个通用 alert 组件

[vue 封装通用的通知组件 alert](https://juejin.cn/post/6844904081085956109)

### 4.封装通用 table 组件

[Vue 封装通用 table 组件](https://juejin.cn/post/6990593017874743310)

```vue
<!-- src/components/table-slot/table.vue -->
<template>
  <table>
    <thead>
      <tr>
        <th v-for="col in columns">{{ col.title }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, rowIndex) in data">
        <td v-for="col in columns">
          <template v-if="'render' in col">
            <Render
              :row="row"
              :column="col"
              :index="rowIndex"
              :render="col.render"
            ></Render>
          </template>
          <template v-else-if="'slot' in col">
            <slot
              :row="row"
              :column="col"
              :index="rowIndex"
              :name="col.slot"
            ></slot>
          </template>
          <template v-else>{{ row[col.key] }}</template>
        </td>
      </tr>
    </tbody>
  </table>
</template>
```

示例中在 `<table-slot>` 内的每一个 `<template>` 就对应某一列的 slot-scope 模板，通过配置的 `slot` 字段，指定具名的 slot-scope。可以看到，基本是把 Render 函数还原成了 html 的写法，这样看起来直接多了，渲染效果是完全一样的。在 slot-scope 中，平时怎么写组件，这里就怎么写，Vue.js 所有的 API 都是可以直接使用的。

```vue
<!-- src/views/table-slot.vue -->
<template>
  <div>
    <table-slot :columns="columns" :data="data">
      <template slot-scope="{ row, index }" slot="name">
        <input type="text" v-model="editName" v-if="editIndex === index" />
        <span v-else>{{ row.name }}</span>
      </template>

      <template slot-scope="{ row, index }" slot="age">
        <input type="text" v-model="editAge" v-if="editIndex === index" />
        <span v-else>{{ row.age }}</span>
      </template>

      <template slot-scope="{ row, index }" slot="birthday">
        <input type="text" v-model="editBirthday" v-if="editIndex === index" />
        <span v-else>{{ getBirthday(row.birthday) }}</span>
      </template>

      <template slot-scope="{ row, index }" slot="address">
        <input type="text" v-model="editAddress" v-if="editIndex === index" />
        <span v-else>{{ row.address }}</span>
      </template>

      <template slot-scope="{ row, index }" slot="action">
        <div v-if="editIndex === index">
          <button @click="handleSave(index)">保存</button>
          <button @click="editIndex = -1">取消</button>
        </div>
        <div v-else>
          <button @click="handleEdit(row, index)">操作</button>
        </div>
      </template>
    </table-slot>
  </div>
</template>
<script>
import TableSlot from "../components/table-slot/table.vue";

export default {
  components: { TableSlot },
  data() {
    return {
      columns: [
        {
          title: "姓名",
          slot: "name",
        },
        {
          title: "年龄",
          slot: "age",
        },
        {
          title: "出生日期",
          slot: "birthday",
        },
        {
          title: "地址",
          slot: "address",
        },
        {
          title: "操作",
          slot: "action",
        },
      ],
      data: [
        {
          name: "王小明",
          age: 18,
          birthday: "919526400000",
          address: "北京市朝阳区芍药居",
        },
        {
          name: "张小刚",
          age: 25,
          birthday: "696096000000",
          address: "北京市海淀区西二旗",
        },
        {
          name: "李小红",
          age: 30,
          birthday: "563472000000",
          address: "上海市浦东新区世纪大道",
        },
        {
          name: "周小伟",
          age: 26,
          birthday: "687024000000",
          address: "深圳市南山区深南大道",
        },
      ],
      editIndex: -1, // 当前聚焦的输入框的行数
      editName: "", // 第一列输入框，当然聚焦的输入框的输入内容，与 data 分离避免重构的闪烁
      editAge: "", // 第二列输入框
      editBirthday: "", // 第三列输入框
      editAddress: "", // 第四列输入框
    };
  },
  methods: {
    handleEdit(row, index) {
      this.editName = row.name;
      this.editAge = row.age;
      this.editAddress = row.address;
      this.editBirthday = row.birthday;
      this.editIndex = index;
    },
    handleSave(index) {
      this.data[index].name = this.editName;
      this.data[index].age = this.editAge;
      this.data[index].birthday = this.editBirthday;
      this.data[index].address = this.editAddress;
      this.editIndex = -1;
    },
    getBirthday(birthday) {
      const date = new Date(parseInt(birthday));
      const year = date.getFullYear();
      const month = date.getMonth() + 1;
      const day = date.getDate();

      return `${year}-${month}-${day}`;
    },
  },
};
</script>
```

### 5.实现 checkbox

```vue
<template>
  <div>
    <span>全选</span>
    <input type="checkbox" v-model="checkAll" />
    <div v-for="(item, index) in test" :key="index">
      <span>{{ item.name }}</span>
      <input type="checkbox" v-model="item.isSelected" />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      test: [
        { name: "测试1", isSelected: true },
        { name: "测试2", isSelected: true },
        { name: "测试3", isSelected: true },
        { name: "测试4", isSelected: true },
        { name: "测试5", isSelected: true },
      ],
    };
  },
  computed: {
    checkAll: {
      get() {
        // 返回什么结果接赋予给 checkAll 属性
        return this.test.every((item) => item.isSelected);
      },
      set(val) {
        // val 是给 checkAll 赋予值的时候传递过来的
        return this.test.forEach((item) => (item.isSelected = val));
      },
    },
  },
};
</script>
```

### 6.实现内容绑定

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<script src="js/vue.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app">
			<h2>{{username}}</h2>
			<h1>单行文本输入框</h1>
			<input type="text" name="username" v-model.lazy.trim="username" value="" />
			<h1>多行文本输入框</h1>
			<textarea rows="" cols="" v-model="username"></textarea>

			<h1>复选框:选择喜欢的水果</h1>
			<span v-for="item in fruits">
				{{item}}
				<input  type="checkbox" name="fruit" v-model="checkFruits" :value="item" />
			</span>
			<h2>{{checkFruits}}</h2>


			<h1>单选框:选择最喜欢的水果</h1>
			<span v-for="item in fruits">
				{{item}}
				<input  type="radio" name="zfruit" v-model="radioFruits" :value="item" />
			</span>
			<h2>{{radioFruits}}</h2>


			<h1>选项框：选择你居住的城市</h1>
			<select v-model="chooseCity">
				<option disabled value="">请选择</option>
				<option v-for="item in citys" :value="item">{{item}}</option>
			</select>
			<h3>{{chooseCity}}</h3>


			<h1>选项框：选择你喜欢的城市</h1>
			<select v-model="moreCity" multiple="multiple">
				<option v-for="item in citys" :value="item">{{item}}</option>
			</select>
			<h3>{{moreCity}}</h3>

			<h1>将字符串变为数字获取</h1>
			<input type="text" name="age" v-model.number="age" value="" />

		</div>

		<script type="text/javascript">
			let app = new Vue({
				el:"#app",
				data:{
					username:"小明",
					fruits:['苹果','雪梨',"香蕉","葡萄"],
					checkFruits:[],
					radioFruits:"",
					citys:['北京',"上海","深圳","广州"],
					chooseCity:"",
					moreCity:[],
					age:16
				},
				watch:{
					age:function(val){
						console.log(val)
					}
				}
			})
		</script>
	</body>
</html>

```

### 7.实现 todolist

```vue
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
    <meta
      name="viewport"
      content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no"
    />
    <link rel="stylesheet" type="text/css" href="css/style.css" />
    <link rel="stylesheet" type="text/css" href="css/animate.min.css" />
    <script src="js/lcXys.js" type="text/javascript" charset="utf-8"></script>
    <script src="js/vue.js" type="text/javascript" charset="utf-8"></script>
  </head>
  <body>
    <div id="app">
      <div class="main">
        <div class="header">
          <div class="logo">LcTodo</div>
          <!-- 绑定回车事件,v-model绑定输入框的value值 -->
          <input
            type="text"
            v-model="inputValue"
            id="input"
            @keydown.enter="enterEvent"
            placeholder="请输入待办事项"
          />
        </div>
        <div class="doing todo">
          <h3><span class="title">正在进行</span><span class="num">0</span></h3>
          <div class="list">
            <transition-group
              name="slide"
              mode="out-in"
              enter-active-class="animated bounceInLeft"
              leave-active-class="animated bounceOutRight"
            >
              <div
                class="todoItem"
                v-for="(item, index) in doingList"
                :key="'doing' + index"
              >
                <input
                  @click.prevent="checkDone(item.id)"
                  :data-id="item.id"
                  type="checkbox"
                />
                <div class="content">{{ item.content }}</div>
                <div class="del" @click="deleteItem(item.id)">删除</div>
              </div>
            </transition-group>
          </div>
        </div>
        <div class="done todo">
          <h3><span class="title">正在进行</span><span class="num">0</span></h3>
          <div class="list">
            <transition-group
              name="slide"
              enter-active-class="animated bounceInLeft"
              leave-active-class="animated bounceOutRight"
            >
              <div
                class="todoItem"
                v-for="(item, index) in doneList"
                :key="'done' + index"
              >
                <input
                  @click.prevent="checkDone(item.id)"
                  :data-id="item.id"
                  type="checkbox"
                  checked="checked"
                />
                <div class="content">{{ item.content }}</div>
                <div class="del" @click="deleteItem(item.id)">删除</div>
              </div>
            </transition-group>
          </div>
        </div>
      </div>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: "#app",
        data: {
          todoList: [],
          inputValue: "",
        },
        computed: {
          //通过过滤todolist数据，得到未做好的列表和已做好的列表
          doingList: function () {
            let arr = this.todoList.filter(function (item, index) {
              return !item.isDone;
            });
            return arr;
          },
          doneList: function () {
            let arr = this.todoList.filter(function (item, index) {
              return item.isDone;
            });
            return arr;
          },
        },
        methods: {
          enterEvent: function (event) {
            //将数据添加至todolist
            this.todoList.push({
              content: this.inputValue,
              isDone: false,
              id: this.todoList.length,
            });
            //保存
            this.saveData();
            //清除输入框的值
            this.inputValue = "";
          },
          // 将数据保存到本地存储
          saveData: function () {
            localStorage.todoList = JSON.stringify(this.todoList);
          },
          checkDone: function (id) {
            //console.log(id)
            this.todoList[id].isDone = !this.todoList[id].isDone;
            //每次修改都必须保存
            this.saveData();
          },
          deleteItem: function (id) {
            this.todoList.splice(id, 1);
            this.todoList.forEach(function (item, i) {
              item.id = i;
            });
            this.saveData();
          },
        },
        mounted: function () {
          this.todoList = localStorage.todoList
            ? JSON.parse(localStorage.todoList)
            : [];
        },
      });
    </script>
  </body>
</html>
```

css

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #efefef;
  font-size: 16px;
}
#app {
  width: 3.75rem;
}
.main {
  width: 3.75rem;
  /* height: 10vh; */
}

.header {
  width: 3.75rem;
  height: 0.5rem;
  background: deepskyblue;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header > .logo {
  width: 1.2rem;
  height: 0.5rem;
  text-align: center;
  line-height: 0.5rem;
  font-size: 0.25rem;
  font-weight: 900;
}
.header > input {
  width: 2.2rem;
  height: 0.3rem;
  margin: 0 0.2rem;
  border-radius: 0.05rem;
  border: none;
  outline: none;
  padding: 0 0.1rem;
}

.todo h3 {
  height: 0.6rem;
  line-height: 0.6rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 0.15rem;
}

.todo .list {
  padding: 0 0.15rem;
}
.todo .todoItem {
  display: flex;
  height: 0.38rem;
  line-height: 0.38rem;
  align-items: center;
  background: lightcyan;
  border-radius: 0.05rem;
  overflow: hidden;
  margin-bottom: 0.1rem;
}
.todo .todoItem:before {
  width: 0.04rem;
  height: 0.38rem;
  background: deepskyblue;
  content: "";
}
.todo .todoItem > input {
  width: 0.25rem;
  height: 0.25rem;
  margin: 0 0.1rem;
}
.todo .todoItem .content {
  width: 2.65rem;
  color: #333;
}
.todo .todoItem .del {
  background: orangered;
  width: 0.4rem;
  height: 0.2rem;
  font-size: 0.12rem;
  text-align: center;
  line-height: 0.2rem;
  border-radius: 0.05rem;
  margin: 0 0.1rem;
  color: #fff;
}

.done.todo .todoItem {
  opacity: 0.3;
  -webkit-filter: grayscale(1);
}

.pc {
  font-size: 200px !important;
}

.pc .main {
  margin: 0 auto;
}
```

### 8.实现简单的弹窗组件实现

基于 Vue 或 React 实现一个弹窗，
1、弹窗带有半透明的全屏遮罩；

2、弹窗可以点击遮罩和关闭按钮隐藏，也可以通过设置 visible 的 prop 隐藏；

3、弹窗可以设置 title 和主内容；

4、弹窗打开和关闭时可以 emit 事件 open 和 close；

5、场景弹窗显示时可以带动画（加分项）；

#### 实现步骤

1. 先搭建组件的 html 和 css 样式，遮罩层和内容层。
2. 定制弹窗内容：弹窗组件通过`slot`插槽接受从父组件那里传过来弹窗内容。
3. 定制弹窗样式：弹窗组件通过`props`接收从父组件传过来的弹窗宽度，上下左右的位置。
4. 组件开关：通过父组件传进来的`props`控制组件的显示与隐藏，子组件关闭时通过事件`$emit`触发父组件改变值。

#### 1.搭建组件的 html 和 css 样式

html 结构：一层遮罩层，一层内容层，内容层里面又有一个头部 title 和主体内容和一个关闭按钮。

下面是组件中的 html 结构，里面有一些后面才要加进去的东西，如果看不懂的话可以先跳过，

```js
<template>
  <div class="dialog">
      <!--外层的遮罩 点击事件用来关闭弹窗，isShow控制弹窗显示 隐藏的props-->
      <div class="dialog-cover back"  v-if="isShow"  @click="closeMyself"></div>
      <!-- transition 这里可以加一些简单的动画效果 -->
      <transition name="drop">
         <!--style 通过props 控制内容的样式  -->
        <div class="dialog-content" :style="{top:topDistance+'%',width:widNum+'%',left:leftSite+'%'}"  v-if="isShow">
          <div class="dialog_head back">
             <!--弹窗头部 title-->
              <slot name="header">提示信息</slot>
          </div>
          <div class="dialog_main" :style="{paddingTop:pdt+'px',paddingBottom:pdb+'px'}">
            <!--弹窗的内容-->
            <slot name="main">弹窗内容</slot>
          </div>
          <!--弹窗关闭按钮-->
          <div  class="foot_close" @click="closeMyself">
              <div class="close_img back"></div>
          </div>
        </div>
    </transition>
  </div>
</template>
```

下面是组件中的主要的 css 样式，里面都做了充分的注释，主要通过`z-index`和`background`达到遮罩的效果，具体内容的 css 可以根据自己的需求来设置。

```js
<style lang="scss" scoped>
 // 最外层 设置position定位
  .dialog {
    position: relative;
    color: #2e2c2d;
    font-size: 16px;
  }
  // 遮罩 设置背景层，z-index值要足够大确保能覆盖，高度 宽度设置满 做到全屏遮罩
  .dialog-cover {
    background: rgba(0,0,0, 0.8);
    position: fixed;
    z-index: 200;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  // 内容层 z-index要比遮罩大，否则会被遮盖，
  .dialog-content{
    position: fixed;
    top: 35%;
    // 移动端使用felx布局
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 300;
 }
</style>
```

#### 2.通过`slot`定制弹窗内容

这一步，只要理解了`slot`的作用以及用法，就没有问题了。

##### 单个插槽：

```js
<slot>这是在没有slot传进来的时候，才显示的弹窗内容</slot>
```

上面是单个插槽也叫默认插槽，在父组件中使用插槽的正确姿势：

```js
<my-component>
   <!--在my-component里面的所有内容片段都将插入到slot所在的DOM位置，并且会替换掉slot标签-->
   <!--这两个p标签，将替换整个slot标签里面的内容-->
    <p>这是一些初始内容</p>
    <p>这是更多的初始内容</p>
  </my-component>
```

ps:如果子组件里面包含`slot`插槽，那么上面的 p 标签的内容将会被丢弃。

##### 具名插槽：

所谓的具名插槽，即为`slot`标签赋一个`name`属性，具名插槽可以父组件中不同的内容片段放到子组件的不同地方，具名插槽还是可以拥有一个默认插槽。下面可以看一下弹窗组件插槽的使用方式：

```js
<div class="dialog_head back ">
  <!--弹窗头部 title-->
  <slot name="header">提示信息</slot>
 </div>
 <div class="dialog_main " :style="{paddingTop:pdt+'px',paddingBottom:pdb+'px'}">
    <!--弹窗的内容-->
    <slot name="main">弹窗内容</slot>
 </div>
```

在父组件中的使用方式：

1. 将弹窗组件引入要使用的组件中，并通过`components`注册成为组件。
2. 父组件中弹窗组件插槽的使用方法如下。

```js
<dialogComponent>
  <div slot="header">插入到name为header的slot标签里面</div>
  <div class="dialog_publish_main" slot="main">
    这里是内容插入到子组件的slot的name为main里面，可以在父组件中添加class定义样式，事件类型等各种操作
  </div>
</dialogComponent>
```

关于组件中用到的插槽的介绍就到这里了，插槽在弹窗组件中的应用是一个典型的栗子，可以看到插槽作用相当强大，而插槽本身的使用并不难，同学们爱上插槽了没有？

#### 3.通过`props`控制弹窗显隐&&定制弹窗 style

`psops`是 Vue 中父组件向子组件传递数据的一种方式，不熟悉的小伙伴们可以看一下[props 文档](https://link.juejin.cn?target=https%3A%2F%2Fcn.vuejs.org%2Fv2%2Fguide%2Fcomponents.html%23Prop)。

因为弹窗组件都是引到别的组件里面去用的，为了适合不同组件场景中的弹窗，所以弹窗组件必须具备一定的可定制性，否则这样的组件将毫无意义,下面介绍一下 props 的使用方式，以弹窗组件为例：

1. 首先需要在被传入的组件中定义 props 的一些特性，验证之类的。
2. 然后在父组件中绑定 props 数据。

```js
<script>
export default {
  props: {
    isShow: {
    //弹窗组件是否显示 默认不显示
      type: Boolean,
      default: false,
      required:true, //必须
    },
    //下面这些属性会绑定到div上面 详情参照上面的html结构
    // 如： :style="{top:topDistance+'%',width:widNum+'%'}"
    widNum:{
    //内容宽度
      type: Number,
      default:86.5
    },
    leftSite:{
      // 左定位
      type: Number,
      default:6.5
    },
    topDistance: {
        //top上边距
      type: Number,
      default:35
    },
    pdt:{
      //上padding
      type: Number,
      default:22
    },
    pdb:{
      //下padding
      type: Number,
      default:47
    }
  },
}
</script>
```

父组件中使用方式：

```js
<dialogComponent :is-show="status.isShowPublish" :top-distance="status.topNum">
 </dialogComponent>
```

ps：props 传递数据不是双向绑定的，而是**单向数据流**，父组件的数据变化时，也会传递到子组件中，这就意外着我们不应该在子组件中修改 props。所以我们在关闭弹窗的时候就**需要通过`$emit`来修改父组件的数据**，然后数据会自动传到子组件中。

现在基本上弹窗组件都已实现的差不多了，还差一个弹窗的关闭事件，这里就涉及到子组件往父组件传参了。

#### 4.`$emit`触发父组件事件修改数据，关闭弹窗

Vue 中在子组件往父组件传参，很多都是通过`$emit`来触发父组件的事件来修改数据。

在子组件中，在点击关闭，或者遮罩层的时候触发下面这个方法：

```js
methods: {
    closeMyself() {
      this.$emit("on-close");
      //如果需要传参的话，可以在"on-close"后面再加参数，然后在父组件的函数里接收就可以了。
    }
  }
```

父组件中的写法：

```js
<dialogComponent :is-show="status.isShowPublish" :top-distance="status.topNum"  @on-close="closeDialog">
  </dialogComponent>
  //"on-close是监听子组件的时间有没有触发，触发的时候执行closeDialog函数
methods:{
  closeDialog(){
    // this.status.isShowPublish=false;
    //把绑定的弹窗数组 设为false即可关闭弹窗
  },
}
```

#### 5.实现点击弹框外关闭弹框功能

[实现点击弹框外关闭弹框功能](https://blog.csdn.net/weixin_43294560/article/details/122701956)

[vue 中实现点击空白区域关闭弹窗](https://juejin.cn/post/6911863086487961607)

核心是监听全局点击事件,通过判断点击时的 dom 元素是否包含在弹框的 dom 中，即弹框

```js
dom.contains(event.target)
<body>
    <div class="modal">Modal</div>
    <script>
        const model = document.querySelector('.modal');
        function toggle(open) {
            model.style.display = open ? 'block' : 'none';
        }
        window.addEventListener('click', (event) => {
            if (!model.contains(event.target)) {
                toggle(false);
            }
        });
    </script>
</body>
```

```js
<template>
  <div>
    <div class="mask" v-if="showModal" @click="showModal=false"></div>
    <div class="pop" v-if="showModal">
        <button @click="showModal=false" class="btn">点击出现弹框</button>
    </div>
    <button @click="showModal=true" class="btn">点击出现弹框</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showModal: false
    };
  }
};
</script>

<style scoped>
.mask {
  background-color: #000;
  opacity: 0.3;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1
}
.pop {
  background-color: #fff;

  position: fixed;
  top: 100px;
  left: 300px;
  width: calc(100% - 600px);
  height:calc(100% - 200px);
  z-index: 2
}
.btn {
  background-color: #fff;
  border-radius: 4px;
  border: 1px solid blue;
  padding: 4px 12px;
}
</style>
```
