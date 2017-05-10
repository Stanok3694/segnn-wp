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
        created() {
            axios.get('src/assets/data/togglers/toggler-style.json')
                .then(response => {
                    this.togglerStyle = response.data.style;
                })
                .catch(e => {
                    console.log('error');
                })
            if(this.toggler == "first"){
                axios.get('src/assets/data/togglers/toggler-first.json')
                .then(response => {
                    this.togglerLink = response.data.link;
                    this.togglerHeader = response.data.header;
                    this.togglerContent = response.data.content;
                })
                .catch(e => {
                    console.log('error');
                })
            }
            if(this.toggler == "second"){
                axios.get('src/assets/data/togglers/toggler-second.json')
                .then(response => {
                    this.togglerLink = response.data.link;
                    this.togglerHeader = response.data.header;
                    this.togglerContent = response.data.content;
                })
                .catch(e => {
                    console.log('error');
                })
            }
            if(this.toggler == "third"){
                axios.get('src/assets/data/togglers/toggler-third.json')
                .then(response => {
                    this.togglerLink = response.data.link;
                    this.togglerHeader = response.data.header;
                    this.togglerContent = response.data.content;
                })
                .catch(e => {
                    console.log('error');
                })
            }
        }
    }
</script>