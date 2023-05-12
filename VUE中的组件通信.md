# Vue 的组件间通信

# Ref 方式

Ref 可以父传子,子传父,但是 vue 官方文档的建议是用来父传子,子传父并未提及

## ref 父传子方式

首先在父组件中引入子组件,将引入的子组件写入到模板当中

在子组件标签上,为其添加 ref 事件`ref="testStudent"`

按钮用来调用父组件内的事件,使其能够调用子组件内的事件

`this.$refs.ref事件名.子组件内的事件名;`
`this.$refs.testStudent.ziMethods();`

### 父组件

```
<template>
  <div>
    <Child ref="testStudent" />
    <button @click="ziAdd">父组件按钮</button>
  </div>
</template>

<script>

// 引入子组件
import Child from '../components/Child_1.vue'
export default {
  name: 'FU',
  data () {
    return {
      data: '父组件内数据'
    }
  },
  components: { Child },

  methods: {
    ziAdd () {
      // 调用子组件事件,并传递数据data
      this.$refs.testStudent.ziMethods(this.data);
    }

  },
}
</script>

<style>
</style>
```

### 子组件

```
<script>
export default {
  name: 'ZI',
  methods: {
    ziMethods (data) {
      console.log('子组件事件被触发,传递的数据为', data)
    }
  }
}
</script>
```

## Ref 子传父

一.父组件引入子组件,为其添加 ref 事件

```
    <Child ref="testStudent" />
```

二.父组件`mounted`监听 ref 事件

`this.$refs.模板ref名.$on("ref自定义事件名", 调用的事件名);`

### 父组件

```
  mounted () {
    // 监听事件
    this.$refs.testStudent.$on('123', message => {
      // 监听子组件发送的消息并响应
      console.log(message)
    })
  },

```

### 子组件

子组件调用父组件内事件,并传递参数

`this.$emit("自定义事件名", 传递的数据);`

```
<template>
  <div>
    <button @click="getStudentName">Ref触发事件</button>
  </div>
</template>

<script>
export default {
  name: 'ZI',
    data () {
    return {
      data: '子组件内数据'
    }
  },
  methods: {
    getStudentName () {
      this.$emit("123", this.data);
    },
  }
}
</script>

```

# 自定义事件方式

## 自定义事件,子传父

### 父组件

```
    <!-- 地图选择器 -->
    <MapWorld v-if="mapIf" v-on:testDemo="demo" />

    ----------------------------------------------------------------

    demo (x) {
      console.log("demo被调用了", x);
    },
```

### 子组件

添加一个点击事件,触发自定义事件,第一个参数为父组件中的自定义参数名,第二个参数为要传递的值

```
      this.$emit("testDemo", this.address);
```
