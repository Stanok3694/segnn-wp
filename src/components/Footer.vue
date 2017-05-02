<template>
    <div>
        <div v-if="divider">
            <hr class="featurette-divider">
        </div>
        <footer>
            <p class="pull-right">
                <a href="#">
                    {{upLinkName}} 
                </a> 
            </p>
            <p>
                &copy; {{currentYear}} {{companyName}} &middot;
            </p>
        </footer>
    </div>
</template>

<script>
    export default {    
        data () {
            return {
                divider: true,
                upLinkName: 'Наверх',
                currentYear: this.getCurrentYear(),
                companyName: 'СтройЭлектроГрупп'
            }
        },
        methods: {
            getCurrentYear: function(){
                return new Date().getFullYear();
            }
        }
    }
</script>