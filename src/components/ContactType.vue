<template>
    <div :class="contactStyle">
        <img class="img-circle"
            :src="contactLink"
            alt="Generic placeholder image"
            width="140" height="140">
        <h2>{{contactHeader}}</h2> 
        <p>{{contactContent}}</p> 
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        props: {
            content: {
                type: String,
                required: true
            }   
        },
        data(){
            return {
                contactLink: "",
                contactStyle: "",                
                contactHeader: "",
                contactContent: ""
            }
        },
        created(){
            axios.get('src/assets/data/contacts/contact-style.json')
                .then(response => {
                    this.contactStyle = response.data.style;
                })
                .catch(e => {
                    console.log('error');
                })
            if(this.content == "first"){
                axios.get('src/assets/data/contacts/contacts-first.json')
                .then(response => {
                    this.contactLink = response.data.link;
                    this.contactHeader = response.data.header;
                    this.contactContent = response.data.content;
                })
                .catch(e => {
                    console.log('error');
                })
            }
            if(this.content == "second"){
                axios.get('src/assets/data/contacts/contacts-second.json')
                .then(response => {
                    this.contactLink = response.data.link;
                    this.contactHeader = response.data.header;
                    this.contactContent = response.data.content;
                })
                .catch(e => {
                    console.log('error');
                })
            }
            if(this.content == "third"){
                axios.get('src/assets/data/contacts/contacts-third.json')
                .then(response => {
                    this.contactLink = response.data.link;
                    this.contactHeader = response.data.header;
                    this.contactContent = response.data.content;
                })
                .catch(e => {
                    console.log('error');
                })
            }
        }
    }
</script>