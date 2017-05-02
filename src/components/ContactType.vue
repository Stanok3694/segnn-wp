<template>
    <div :class="feature">
        <img class="img-circle"
            :src="source"
            alt="Generic placeholder image"
            width="140" height="140">
        <h2>{{header}}</h2> 
        <p>{{content}}</p> 
    </div>
</template>

<script>
    export default {
        props: {
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
        }
    }
</script>