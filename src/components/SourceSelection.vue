<template>
    <div class='sourceSelection'>
        <div class='jumbotron'>
            <h2> <span class='glyphicon glyphicon-list-alt'></span> New List</h2>
            <!-- https://cdn3.iconfinder.com/data/icons/linecons-free-vector-icons-pack/32/news-48.png -->
            <h4>Select News Source</h4>
            <select class='form-control' v-on:click='sourceChanged'>
                <option v-bind:value="source.id" v-for='source in sourcesArr'>{{source.name}}</option>
            </select>

            <div v-if='source'>
                <h6>{{source.description}}</h6>
                <a v-bind:href="source.url" class='btn btn-primary' target='_blank'>Go To {{source.name}}</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'sourceSelection',
    data() {
        return {
            title: 'Source',
            sourcesArr: [],
            source: ''
        }
    },
    methods: {
        sourceChanged(event) {
            for(let i=0; i<this.sourcesArr.length; i++) {
                if(this.sourcesArr[i].id == event.target.value) {
                    this.source = this.sourcesArr[i];
                }
            }
            this.$emit('sourceChanged', event.target.value)
            // console.log(event.target.value)
        }
    },
    created: function() {
        this.$http.get('https://newsapi.org/v1/sources?language=en').
        then(response => {
            this.sourcesArr = response.data.sources;
            console.log(response.data.sources)
        })
    }
}
</script>
<style scoped>
    
</style>