<template>
    <div>
        <transition name="fade">
            <Modal @closeModal="모달창열렸니 = false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
        </transition>

        <div class="menu">
            <a v-for="i in 메뉴들" :key="i">{{ i }}</a>
        </div>

        <Discount v-if="showDiscount == true" :할인율="할인율" />

        <button @click="lowPriceSort">낮은 가격순</button>
        <button @click="highPriceSort">높은 가격순</button>
        <button @click="alphabeticalSort">가나다순</button>
        <button @click="sortBack">되돌리기</button>

        <!-- <div v-for="(a,i) in 3" :key="i">
            <h4>{{ products[i] }}</h4>
            <p>70 만원</p>
        </div> -->

        <!-- <div v-for="(a, i) in products" :key="i">
            <h4>{{ a }}</h4>
            <p>70 만원</p>
        </div> -->

        <Card @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(작명,i) in 원룸들" :key="작명" />

        <!-- <Card :원룸="원룸들[1]" />
        <Card :원룸="원룸들[2]" />
        <Card :원룸="원룸들[3]" />
        <Card :원룸="원룸들[4]" />
        <Card :원룸="원룸들[5]" /> -->

        <!-- <div v-for="(a, i) in 원룸들" :key="i">
            <img :src="a.image" class="room-img">
            <h4 @click="모달창열렸니 = true; 누른거 = i">{{ a.title }}</h4>
            <p>{{ a.price }}원</p>
            <button v-on:click="신고수[0]++">허위매물신고</button> <span>신고수: {{ 신고수[0] }}</span>
        </div> -->
        <!-- <div>
            <img src="./assets/room1.jpg" class="room-img">
            <h4>{{ products[1] }}</h4>
            <p>60만원</p>
            <button v-on:click="신고수[1]++">허위매물신고</button> <span>신고수: {{ 신고수[1] }}</span>
        </div>
        <div>
            <img src="./assets/room2.jpg" class="room-img">
            <h4>{{ products[2] }}</h4>
            <p>70만원</p>
            <button v-on:click="신고수[2]++">허위매물신고</button> <span>신고수: {{ 신고수[2] }}</span>
        </div> -->
    </div>
</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
    name: 'App',
    data(){
        return {
            할인율 : 30,
            showDiscount : true,
            원룸들오리지널 : [...data],
            누른거 : 0,
            원룸들 : data,
            모달창열렸니 : false,
            신고수 : [0, 0, 0],
            메뉴들 : ['Home', 'Shop', 'About'],
            products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
        }
    },
    methods: {
        increase(){
            this.신고수 += 1;
        },
        sortBack(){
            this.원룸들 = [...this.원룸들오리지널];
        },
        lowPriceSort(){
            this.원룸들.sort(function(a, b){
                return a.price - b.price
            })
        },
        highPriceSort(){
            this.원룸들.sort(function(a, b){
                return b.price - a.price
            })
        },
        alphabeticalSort(){
            this.원룸들.sort(function(a, b){
                return a.title.localeCompare(b.title)
            })
        },
    },

    mounted(){
        this.timer = setInterval(() => {
            this.할인율--;
            if(this.할인율 < 1) {
                clearInterval(this.timer);
            }
        }, 1000);
    },

    components: {
        Discount : Discount,
        Modal : Modal,
        Card : Card,
    }
}
</script>

<style>
.fade-leave-from {
    opacity: 1;
}

.fade-leave-active {
    transition: all 1s;
}

.fade-leave-to {
    opacity: 0;
}

.fade-enter-from {
    opacity: 0;
}

.fade-enter-active {
    transition: all 1s;
}

.fade-enter-to {
    opacity: 1;
}

body {
    margin: 0;
}

div {
    box-sizing: border-box;
}

.discount{
    background: #eee;
    padding: 10px;
    margin: 10px;
    border-radius: 5px;
}

.black-bg {
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    position: fixed;
    padding: 20px;
}

.white-bg {
    width: 100%;
    background: white;
    border-radius: 8px;
    padding: 20px;
}

.room-img {
    width: 100%;
    margin-top: 40px;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

.menu {
    background: darkslateblue;
    padding: 15px;
    border-radius: 5px;
}

.menu a {
    color: white;
    padding: 10px;
}
</style>
