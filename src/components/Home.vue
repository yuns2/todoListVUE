<template>
<v-container>
  <v-layout row wrap>
    <v-flex xs12 text-xs-center>
      <h1>To do List</h1>
      <p>
        전체 할일 : {{ todoList.length }} / 
        완료한 할일 : {{ countDone }} / 
        남은 할일 : {{ todoList.length - countDone }}
      </p>
    </v-flex>
    <v-flex xs6 pa-2>
      <List 
        :todoList="todoList"
        @statusControl="statusControl"
        @deleteList="deleteList"
      ></List>
    </v-flex>
    <v-flex xs6 pa-2>
      <ListAdd 
        @listAdd="listAdd"
        @editContent="editContent"
      ></ListAdd>
    </v-flex>
  </v-layout>
</v-container>
</template>
<script>
import List from "./List";
import ListAdd from "./ListAdd";
export default{
  components : { List, ListAdd },
  data(){
    return {
      todoList : []
    }
  },
  methods : {
    listAdd(memo){
      this.todoList.push({memo:memo, status:'created'})
    },
    statusControl(index, status){
      this.todoList[index].status = status;
    },
    deleteList(index){
      this.todoList.splice(index, 1)
    },
    editContent(memo, index){
      this.todoList[index].memo = memo;
    }
  },
  computed : {
    countDone (){
      let count = 0;
      this.todoList.forEach(list => {
        if(list.status === 'done') count++
      })
      return count;
    }
  }
}
</script>