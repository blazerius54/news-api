<template>
    <div class='newsList'>
        <div class='loading' v-if='isLoading'>
            <div class="loader" >
                <div id="largeBox"></div>
                <div id="smallBox"></div>
            </div>
            <h3>Loading</h3>
        </div>
        <div class="container" v-if='!isLoading'>
            <ul class="media-list">
                <li class='media' v-for='article in articles'>
                    <div class="media-left">
                        <a v-bind:href="article.url" target='_blank'>
                            <img v-bind:src="article.urlToImage" class='media-object'>
                        </a>
                    </div>
                    <div class="media-body">
                        <h4 class='media-heading'>
                            <a v-bind:href="article.url" target='_blank'>{{article.title}}</a>
                        </h4>
                        <h5><i>by {{article.author}}</i></h5>
                        <p>{{article.description}}</p>
                    </div>
                </li>
            </ul>
        </div>
    </div>

</template>

<script>
export default {
    name: 'newsList',
    props: ['src'],     
    data() {
        return {
            title: 'News',
            articles: [],
            isLoading: false
        }
    },
    methods: {
        updataeSource: function(src) {
            this.isLoading = true;
            this.$http.get('https://newsapi.org/v1/articles?source=' + src + '&apiKey=e617d7c5a0fb4bd0aeac3feaaff6a64c').
            then(response => {
                this.articles = response.data.articles;
                this.isLoading= false
            })
        }
    },
    created: function() {
        this.updataeSource(this.src)
    },
    watch: {
        src: function(val) {
            this.updataeSource(val);
        }
    }
    
}
</script>
<style scoped>
.media-object{
    width: 128px;
    padding: 10px
}
.media{
    border-top: 1px solid lightgray;
    padding-top: 20px;
}
body {
    background-color: #34495e;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
    margin: 0;
}

.loading{
    /* display: inline-block; */
    width: 20%;
    margin: 20px auto;
}

.loading h3{
    margin-left: 30%
}

.loader {
    margin: 20px 40%;
    width: 3em;
    height: 3em;
    animation: loaderAnim 1.25s infinite;
    outline: 1px solid transparent;
}
.loader #largeBox {
    height: 3em;
    width: 3em;
    background-color: #ECECEC;
    outline: 1px solid transparent;
    position: fixed;
}
.loader #smallBox {
    height: 3em;
    width: 3em;
    background-color: #34495e;
    position: fixed;
    z-index: 1;
    outline: 1px solid transparent;
    animation: smallBoxAnim 1.25s alternate infinite ease-in-out;
}

@keyframes smallBoxAnim {
    0% {
        transform: scale(0.2);
    }
    100% {
        transform: scale(0.75);
    }
}
@keyframes loaderAnim {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(90deg);
    }
}

</style>