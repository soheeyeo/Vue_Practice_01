<template>
    <div>
        <div class="menu">
            <a v-for="i in 메뉴들" :key="i">{{ i }}</a>
        </div>

        <!-- <div v-for="(a,i) in 3" :key="i">
            <h4>{{ products[i] }}</h4>
            <p>70 만원</p>
        </div> -->

        <!-- <div v-for="(a, i) in products" :key="i">
            <h4>{{ a }}</h4>
            <p>70 만원</p>
        </div> -->

        <div>
            <h4>{{ products[0] }}</h4>
            <p>50만원</p>
            <button v-on:click="increase">허위매물신고</button> <span>신고수: {{ 신고수 }}</span>
        </div>
                <div>
            <h4>{{ products[1] }}</h4>
            <p>60만원</p>
        </div>
                <div>
            <h4>{{ products[2] }}</h4>
            <p>70만원</p>
        </div>
    </div>
</template>

<script>

export default {
    name: 'App',
    data(){
        return {
            신고수 : 0,
            메뉴들 : ['Home', 'Shop', 'About'],
            products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
        }
    },
    methods: {
        increase(){
            this.신고수 += 1;
        }
    },
    components: {
    
    }
}
</script>

<style>
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
