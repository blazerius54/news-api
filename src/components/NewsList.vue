<template>
    <div class='newsList'>
        <div class="container">
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
            articles: []
        }
    },
    methods: {
        updataeSource: function(src) {
            this.$http.get('https://newsapi.org/v1/articles?source=' + src + '&apiKey=e617d7c5a0fb4bd0aeac3feaaff6a64c').
            then(response => {
                this.articles = response.data.articles;
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
</style>