<template>
    <div>
        <div v-if="divider">
            <hr class="featurette-divider">
        </div>
        <div :class="featureType" v-if="visibility">
            <h2 class="featurette-heading">
                {{featureHeader}}
            </h2>
            <p class="lead">
                {{featureContent}}
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
            // getting styles
            if(this.feature == "first"){
                axios.get('src/assets/data/default-feature-contents/feature-style.json')
                    .then(response => {
                        this.featureType = response.data.first;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.feature == "second"){
                axios.get('src/assets/data/default-feature-contents/feature-style.json')
                    .then(response => {
                        this.featureType = response.data.second;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            // getting default contents
            if(this.content == "first"){
                axios.get('src/assets/data/default-feature-contents/feature-first.json')
                    .then(response => {
                        this.featureHeader = response.data.header;
                        this.featureContent = response.data.content;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.content == "second"){
                axios.get('src/assets/data/default-feature-contents/feature-second.json')
                    .then(response => {
                        this.featureHeader = response.data.header;
                        this.featureContent = response.data.content;
                    })
                    .catch(e => {
                        console.log('error');
                    })
            }
            if(this.content == "third"){
                axios.get('src/assets/data/default-feature-contents/feature-third.json')
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