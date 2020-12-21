<template>
<div>
<h3>To do List</h3>
<v-card 
    class="pa-3 mb-3"
    :class="{'done': list.status === 'done'}"
    v-for="(list, index) in todoList"
    :key="index">
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
        @click="$emit('listDelete', index)">
        <i class="fas fa-trash-alt"></i>
    </v-btn>
    <v-btn fab flat small color="orange"
        v-if="list.status === 'created'"
        @click="editList(list.memo, index)">
        <i class="fas fa-edit"></i>
    </v-btn>

</v-card>
</div>
</template>
<script>
import { eventBus } from "../main"
export default{
    props : ["todoList"],
    methods : {
        editList(memo, index){
            eventBus.listEdit(memo, index);
        },
    }
}
</script>

<style scoped>
/* scoped -> list.vue 파일에서만 작동하게 됨 */
.done{
    background-color:rgba(0,0,0,0.1);
}
.done p {
    text-decoration : line-through;
    color : rgba(0,0,0,0.5);
}
</style>