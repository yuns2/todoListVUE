<template>
<v-container>
  <v-layout row wrap>
    <v-flex xs12 text-xs-center> 
      <h1>투두리스트</h1>
      <p>
        전체 할일: {{ todoList.length }} / 
        완료된 할일: {{ countDone }} / 
        남은 할일: {{ todoList.length - countDone }}
      </p>
    </v-flex>
    <v-flex xs6 pa-2>
      <List :todoList="todoList"
        @statusControl="statusControl"
        @listDelete="listDelete"></List>
    </v-flex>
    <v-flex xs6 pa-2>
      <ListAdd
      @listAdd="paintList"
      @listEdit2="listEdit2"
      ></ListAdd>
    </v-flex>
  </v-layout>
</v-container>
</template>
<script>
import List from "./List";
import ListAdd from "./ListAdd";
export default{
  components:{
    List, ListAdd
  },
  data(){
    return {
      todoList : []
    }
  },
  computed : {
    countDone(){
      let count = 0;
      this.todoList.forEach ( list => {
        if(list.status === "done") count++
      })
      return count
    }
  },

  methods :{
    paintList(memo){
      this.todoList.push({memo:memo, status:'created'});
    },
    statusControl(index, status){
      this.todoList[index].status = status;
    },
    listDelete(index){
      // todoList에서 n번째 요소를 찾은 다음, 거기서부터 1개를 지워줘
      this.todoList.splice(index, 1)
    },
    listEdit2(memo, index){
      this.todoList[index].memo = memo;
    }
  }
}
</script>