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
    import axios from 'axios';
    export default {
        data () {
            return {
                divider: '',
                upLinkName: '',
                companyName: '',
                currentYear: this.getCurrentYear()
            }
        },
        methods: {
            getCurrentYear: function(){
                return new Date().getFullYear();
            }
        },
        created() {
            axios.get('src/assets/data/footer.json')
                .then(response => {
                    this.companyName = response.data.companyName;
                    this.upLinkName = response.data.upLinkName;
                    this.divider = response.data.divider;
                })
                .catch(e => {
                    console.log('error');
                })
        }
    }
</script>