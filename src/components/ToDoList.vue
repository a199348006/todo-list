<template>
  <div class="wrapper">
    <el-input class="todo-input" placeholder="輸入待辦事項" v-model="input" @keyup.enter="addItem">
      <template #prepend>
        <el-button circle @click="addItem()"><el-icon :size="20"><CirclePlus /></el-icon></el-button>
      </template>
    </el-input>

    {{ input }}

    <el-card class="todo-list">
      <template #header>
        <span>未完成</span>
        <el-badge :value="todoItem.length" class="item"></el-badge>
      </template>
      <div v-for="(todo, index) in todoItem" :key="index">
        {{ index }} {{ todo }}
        <el-button type="success" size="mini" circle @click="completeItem(index, todo)"><el-icon :size="20"><Check /></el-icon></el-button>         
        <el-button type="danger" size="mini" circle @click="removeItem(index)"><el-icon :size="20"><Minus /></el-icon></el-button>    
      </div>
    </el-card>

    <el-card class="todo-list">
      <template #header>
        <span>完成</span>
        <el-badge :value="doneItem.length" class="item"></el-badge>
      </template>
      <div v-for="(done, index) in doneItem" :key="index">
        {{ index }} {{ done }}
        <el-button type="primary" size="mini" circle @click="back2todo(index, done)"><el-icon :size="20"><RefreshLeft /></el-icon></el-button> 
      </div>
    </el-card>    
      
  </div>
</template>

<script>
import { Check, Minus, CirclePlus, RefreshLeft } from '@element-plus/icons'

export default {
  name: 'ToDoList',
  components: { Check, Minus, CirclePlus, RefreshLeft },
  data() {
    return {
      input: '',
      todoItem: [],
      doneItem: []
    }
  },
  methods: {
    addItem() {
      if(this.input === '') { return }
      this.todoItem.push(this.input)
      this.input = ''
    },
    removeItem(index) {
      this.todoItem.splice(index, 1)
    },
    completeItem(index, item) {
      this.removeItem(index)
      this.doneItem.push(item)
    },
    back2todo(index, item) {
      this.doneItem.splice(index, 1)
      this.todoItem.push(item)
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 765px;
  margin: 0 auto;
}

.todo-input {
  margin: 10px 0px;
}

.todo-list {
  margin: 10px 0px;
}
</style>
