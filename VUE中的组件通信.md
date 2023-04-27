# Vue 的组件间通信

## Ref 方式

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
