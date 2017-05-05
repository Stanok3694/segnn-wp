<template>
    <div :class="togglerStyle">
        <img class="img-circle"
            :src="togglerLink" 
            alt="Generic placeholder image"
            width="140" height="140">
        <h2>{{togglerHeader}}</h2>
        <p>{{togglerContent}}</p>
        <p> 
            <a class="btn btn-default" role="button" href="#feature"> 
                Подробнее &raquo; 
            </a>
        </p>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        props: {
            toggler: {
                type: String,
                required: true
            }       
        },
        data(){
            return {
                togglerContent: '',
                togglerHeader: '',
                togglerStyle: '',
                togglerLink: ''
            }
        },
        methods: {
            setFeatureTogglerLink: function(){
                if(this.toggler == 'first'){
                    this.togglerLink = this.links.first
                }
                if(this.toggler == 'second'){
                    this.togglerLink = this.links.second
                }
                if(this.toggler == 'third'){
                    this.togglerLink = this.links.third
                }
            },
            setFeatureTogglerHeader: function(){
                if(this.toggler == 'first'){
                    this.togglerHeader = this.headers.first
                }
                if(this.toggler == 'second'){
                    this.togglerHeader = this.headers.second
                }
                if(this.toggler == 'third'){
                    this.togglerHeader = this.headers.third
                }
            },
            setFeatureTogglerContent: function(){
                if(this.toggler == 'first'){
                    this.togglerContent = this.contents.first
                }
                if(this.toggler == 'second'){
                    this.togglerContent = this.contents.second
                }
                if(this.toggler == 'third'){
                    this.togglerContent = this.contents.third
                }
            }
        },
        created() {
            if(this.toggler == "first"){
                axios.get('src/assets/data/toggler.json')
                .then(response => {
                    this.togglerLink = response.data.first.link;
                    this.togglerHeader = response.data.first.header;
                    this.togglerContent = response.data.first.content;
                    this.togglerStyle = response.data.style;
                })
                .catch(e => {
                    console.log('error');
                })
            }
        }
    }
</script>