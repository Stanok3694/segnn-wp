<template>
    <div>
        <hr class="featurette-divider">
        <h2 align="center">{{projectHeader}}</h2>
        <div class="wrapper">
            <div :class="projectStyle" id="card" v-for="project in projectContent">
              <p>{{project.owner}}</p>
              <p>{{project.name}}</p>
              <p>{{project.data}}</p>
            </div>
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
            }
        },
        data(){
            return {
                projectStyle: "",
                projectHeader: "",
                projectContent: {}
            }
        },
        created(){
            axios.get('src/assets/data/projects/projects-style.json')
                .then(response => {
                    this.projectStyle = response.data.style                    
                })
                .catch(e => {
                    console.log('error')
                })
            if(this.content == "project"){
                axios.get('src/assets/data/projects/projects-first.json')
                    .then(response => {
                        this.projectContent = response.data.projects;
                        this.projectHeader = response.data.header;
                    })
                    .catch(e => {
                        console.log('error')
                    })                
            }
            if(this.content == "wiring"){
                axios.get('src/assets/data/projects/projects-second.json')
                    .then(response => {
                        this.projectContent = response.data.wirings;
                        this.projectHeader = response.data.header;
                    })
                    .catch(e => {
                        console.log('error')
                    })                
            }
            if(this.content == "audit"){
                axios.get('src/assets/data/togglers/projects-third.json')
                    .then(response => {
                        this.projectContent = response.data.energoAudit;
                        this.projectHeader = response.data.header;
                    })
                    .catch(e => {
                        console.log('error')
                    })                
            }
        }
    }

</script>