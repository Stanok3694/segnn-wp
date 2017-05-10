<template>
    <div :class="imageStyle" v-if= "visibility">
        <img class="featurette-image img-responsive center-block" 
            :src="imageSource"
            alt="Generic placeholder image">
    </div>
</template>

<script>
    import axios from 'axios';
    export default {    
        props: {
            visibility: {
                type: Boolean,
                required: true
            },
            source: {
                type: String,
                required: true
            },
            feature: {
                type: String,
                required: true
            }
        },
        data(){
            return {
                imageStyle: "",
                imageSource: ""
            }
        },
        created(){
            // getting styles
            if(this.feature == "first"){
                axios.get('src/assets/data/default-feature-images/image-style.json')
                    .then(response => {
                        this.imageStyle = response.data.first;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.feature == "second"){
                axios.get('src/assets/data/default-feature-images/image-style.json')
                    .then(response => {
                        this.imageStyle = response.data.second;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            // getting images
            if(this.feature == "first"){
                axios.get('src/assets/data/default-feature-images/image-first.json')
                    .then(response => {
                        this.imageSource = response.data.link;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.feature == "second"){
                axios.get('src/assets/data/default-feature-images/image-second.json')
                    .then(response => {
                        this.imageSource = response.data.link;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.feature == "third"){
                axios.get('src/assets/data/default-feature-images/image-third.json')
                    .then(response => {
                        this.imageSource = response.data.link;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
        }
    }
</script>