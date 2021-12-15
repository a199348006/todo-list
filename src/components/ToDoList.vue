<template>
  <div class="wrapper">
    <el-input class="todo-input" placeholder="輸入待辦事項" v-model="input" @keyup.enter="addItem">
      <template #prepend>
        <el-button circle @click="addItem()"><el-icon :size="20"><CirclePlus /></el-icon></el-button>
      </template>
    </el-input>

    <el-card class="todo-list">
      <template #header>
        <span>未完成</span>
        <el-badge :value="todoItem.length"></el-badge>
      </template>
      <div v-for="(todo, index) in todoItem" :key="index" class="item">
        <el-row>
          <el-col :span="20" class="item-title">{{ todo }}</el-col>
          <el-col :span="4" class="item-button">
            <el-button type="success" size="mini" circle @click="completeItem(index, todo)"><el-icon :size="20"><Check /></el-icon></el-button>         
            <el-button type="danger" size="mini" circle @click="removeItem(index)"><el-icon :size="20"><Minus /></el-icon></el-button> 
          </el-col>
        </el-row>
      </div>
    </el-card>    

    <el-card class="todo-list">
      <template #header>
        <span>完成</span>
        <el-badge :value="doneItem.length"></el-badge>
      </template>
      <div v-for="(done, index) in doneItem" :key="index" class="item done" style="border-color: #708090;">
        <el-row>
          <el-col :span="20" class="item-title">{{ done }}</el-col>
          <el-col :span="4" class="item-button">
            <el-button type="primary" size="mini" circle @click="back2todo(index, done)"><el-icon :size="20"><RefreshLeft /></el-icon></el-button> 
          </el-col>
        </el-row>
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

.item {
  border-width: 1px;
  border-color: #FF8C00;
  border-style: solid;
  padding: 3px;
  margin: 2px 0px;
}

.item-title {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  word-break: break-all;
}

.item-button {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.done {
  background-color: #CDCDCD;
}
</style>
