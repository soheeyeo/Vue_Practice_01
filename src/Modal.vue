<template>
    <div class="black-bg" v-if="모달창열렸니 == true">
        <div class="white-bg">
            <h4>{{ 원룸들[누른거].title }}</h4>
            <img :src="원룸들[누른거].image" class="room-img">
            <p>{{ 원룸들[누른거].content }}</p>
            <input v-model="month">
            <p> {{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }} 원</p>

            <button @click="$emit('closeModal')">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
    name : 'ModalVue',
    data(){
        return {
            month : 1,
        }
    },
    watch : {
        month(a) {
            if (isNaN(a) == true){
                alert('숫자만 입력해주세요');
                this.month = 1;
            }
        },
    },
    beforeUpdate(){
        if(this.month == 2){
            alert('3개월 이상 가능합니다.')
            this.month = 3;
        }
    },
    props : {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,
    }
}
</script>

<style>

</style>