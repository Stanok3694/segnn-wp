<template>
    <div :class="feature" v-if= "visibility">
        <img class="featurette-image img-responsive center-block" 
            :src="source"
            alt="Generic placeholder image">
    </div>
</template>

<script>
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
        }
    }
</script>