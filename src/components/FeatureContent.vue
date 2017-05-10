<template>
    <div>
        <div v-if="divider">
            <hr class="featurette-divider">
        </div>
        <div :class="featureType" v-if="visibility">
            <h2 class="featurette-heading">
                {{header}}
            </h2>
            <p class="lead">
                {{content}}
            </p>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        props: {
            content: {
                type: String,
                required: true
            },
            feature: {
                type: String,
                required: true
            },
            visibility: {
                type: Boolean,
                required: true
            },
            divider: {
                type: Boolean,
                required: true
            }
        },
        data(){
            return {
               featureType: "",
               featureHeader: "",
               featureContent: ""
            }
        },
        created(){
            if(this.feature == "first"){
                axios.get('src/assets/data/feature-contents/feature-style.json')
                    .then(response => {
                        this.featureType = response.data.first;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.feature == "second"){
                axios.get('src/assets/data/feature-contents/feature-style.json')
                    .then(response => {
                        this.featureType = response.data.second;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.content == "first"){
                axios.get('src/assets/data/feature-contents/feature-first.json')
                    .then(response => {
                        this.featureHeader = response.data.header;
                        this.featureContent = response.data.content;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.content == "second"){
                axios.get('src/assets/data/feature-contents/feature-second.json')
                    .then(response => {
                        this.featureHeader = response.data.header;
                        this.featureContent = response.data.content;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.content == "third"){
                axios.get('src/assets/data/feature-contents/feature-third.json')
                    .then(response => {
                        this.featureHeader = response.data.header;
                        this.featureContent = response.data.content;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
        }
    }
</script>