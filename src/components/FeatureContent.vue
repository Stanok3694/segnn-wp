<template>
    <div>
        <div v-if="divider">
            <hr class="featurette-divider">
        </div>
        <div :class="feature" v-if="visibility">
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
                // Does this need?
            }
        }
    }
</script>