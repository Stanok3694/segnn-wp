<template>
    <div :class="feature">
        <img class="img-circle"
            :src="source" 
            alt="Generic placeholder image"
            width="140" height="140">
        <h2>{{header}}</h2>
        <p>{{content}}</p>
        <p> 
            <a class="btn btn-default" role="button" href="#feature" @click.native="changeFeatureBlock"> 
                Подробнее &raquo; 
            </a>
        </p>
    </div>
</template>

<script>
    export default {
        props: {
            toggler: {
                type: String,
                required: true
            },
            header: {
                type: String,
                required: true
            },
            content: {
                type: String,
                required: true
            },
            feature: {
                type: String,
                required: true
            },
            source: {
                type: String,
                required: true
            }        
        },
        data(){
            return {
                togglerType: this.toggler,
                superClick: this.changeFeatureBlock()
            }
        },
        methods: {
            changeFeatureBlock: function(){
                if(this.tooglerType == "firstFeatureToggler"){
                    this.$emit('selectFirstFeatureBlock')
                }
                if(this.tooglerType == "secondFeatureToggler"){
                    this.$emit('selectSecondFeatureBlock')
                }
                if(this.tooglerType == "thirdFeatureToggler"){
                    this.$emit('selectThirdFeatureBlock')
                }
            }.bind(this)
        }
    }
</script>