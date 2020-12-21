<template>
<div>
    <v-textarea
        v-model="memo"
        label="할일을 입력하세요."
        value=""
    >
    </v-textarea>
    <v-btn
        v-if="mode==='add'"
        @click="listAdd">제출하기</v-btn>
    <v-btn
        v-else
        @click="editContent">수정하기</v-btn>
</div>
</template>
<script>
import { eventBus } from "../main";
export default {
    data(){
        return {
            memo:null,
            index:null,
            mode:'add'
        }
    },
    methods : {
        listAdd(){
            if(this.memo===null){
                alert ("할일을 입력하세요.");
            }else{
                this.$emit('listAdd', this.memo);
                this.memo = null;
            }
        },
        editContent(){
            this.$emit('editContent', this.memo, this.index);
            this.memo = null;
            this.mode = 'add';
        }
    },
    created(){
        eventBus.$on('editCard', (memo, index) => {
            this.memo = memo;
            this.index = index;
            this.mode = 'edit';
        })
    }
}
</script>