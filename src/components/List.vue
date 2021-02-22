<template>
<div>
    <!-- {{ todoList }} -->
    <v-card
        v-for="(list, index) in todoList"
        :key="index"
        class="pa-3 mb-3"
        :class="{'done' : list.status === 'done'}"
    >
        <p>{{ list.memo }}</p>
        <v-btn fab flat small color="green"
            v-if="list.status === 'created'"
            @click="$emit('statusControl', index, 'done')">
            <i class="fas fa-check"></i>
        </v-btn>
        <v-btn fab flat small color="blue"
            v-else
            @click="$emit('statusControl', index, 'created')">
            <i class="fas fa-redo-alt"></i>
        </v-btn>
        <v-btn fab flat small color="red"
            @click="$emit('deleteList', index)">
            <i class="fas fa-trash-alt"></i>
        </v-btn>
        <v-btn fab flat small color="orange"
            v-if="list.status==='created'"
            @click="editCard(list.memo, index)"
        >
            <i class="fas fa-edit"></i>
        </v-btn>
    </v-card>
</div>
</template>
<script>
import { eventBus } from "../main";
export default{
    props : ['todoList'],
    methods : {
        editCard(memo, index){
            // console.log("Hi");
            eventBus.listEdit(memo, index);
        }
    }
}
</script>
<style scoped>
.done {background-color: rgba(0,0,0,0.1);}
.done p {
    color: black;
    text-decoration : line-through;
}
</style>