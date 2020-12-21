<template>
<div>
    <h3>목록을 추가할 수 있습니다.</h3>
    <v-textarea
        outlined
        v-model="memo"
        label="할일을 입력하세요."
        value=""
        ></v-textarea>
    <v-btn v-if="mode==='add'" @click="listAdd">제출하기</v-btn>
    <v-btn v-else @click="listEdit2">수정하기</v-btn>
</div>
</template>
<script>
import { eventBus } from "../main";
export default{
    data(){
        return{
            memo: null,
            index : null,
            mode : 'add'
        }
    },
    methods : {
        listAdd (){
            this.$emit("listAdd", this.memo);
            this.memo = null;
        },
        listEdit2 (){
            if(this.memo === null){
                alert ("할일을 입력해주세요.")
            }else{
                this.$emit("listEdit2", this.memo, this.index);
                // 밑에는 처음 상태로 초기화하기 위한것임
                this.memo = null;
                this.mode = 'add'
            }
        }
    },
    created (){
        eventBus.$on("listEdit", (memo, index) =>
        {
            // console.log(memo, index);
            this.memo = memo;
            this.index = index;
            this.mode = 'edit';
        })
    }
}
</script>