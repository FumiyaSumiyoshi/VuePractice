<template>
  <h1>ToDo</h1>
  <input type="text" v-model="input.task" /><button v-on:click="addToDo">ADD</button><button  v-on:click="deleteToDo">DELETE</button>
  <p v-if="empty != ''">{{ empty.message }}</p>
  <p v-if="toDos.length === 0">登録中のタスクなし</p>
  <ul>
    <li v-for="(toDo, key) in toDos" :key="key">
      <!-- 詰まってしまったこと -->
      <!-- v-model="toDo.doneをv-model="input.doneとしてしまっていたから、
       　　 チェックボックスの押下による取り消し線が1つ押した時に全てに反映されてしまっていた。 -->
      <input type="checkbox" v-model="toDo.done" /><span v-bind:class="{ 'todo-done': toDo.done }">{{ toDo.task }}</span>
    </li>
  </ul>
</template>

<style>
body {
  background-color: #eee;
}

.todo-done {
  text-decoration: line-through;
}
</style>

<script>
export default {
  data() {
    return {
      input: {
        task: '',
        done: false,
      },
      toDos: [],
      empty: {
        message: '',
      },
    }
  },
  methods: {
    addToDo() {
      if(this.input.task != '') {
        this.toDos.push(this.input)
        this.input = {
          task: '',
          done: false,
        }
        this.empty = {
          message: '',
        }
        } else {
          this.empty = {
            message: 'タスクを入力してから登録ボタンを押下してください！！',
          }
      }
    },
    deleteToDo() {
      //delete押下時の配列の長さを取得
      var firstLength = this.toDos.length;
      //checkがついていないものをtoDosに追加する
      for(var i=0; i<firstLength; i++) {
        console.log(this.toDos[i].task);
        if(!this.toDos[i].done) {
          this.toDos.push(this.toDos[i])
        }
      }
      //delete押下前の要素を削除する
      this.toDos.splice(0, firstLength);
    },
  },
}
</script>
