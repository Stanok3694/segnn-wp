<template>
    <div class="navbar-wrapper">
      <div class="container">
        <nav class="navbar navbar-inverse navbar-static-top">
          <div class="container">
            <div class="navbar-header">
              <button type="button" class="navbar-toggle collapsed"
                    data-toggle="collapse" data-target="#navbar"
                    aria-expanded="false" aria-controls="navbar">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
              </button>
              <a class="navbar-brand" >{{companyName}}</a>
            </div>
            <div id="navbar" class="navbar-collapse collapse">
              <ul class="nav navbar-nav">
                <li class="active" ><a href="#" @click="resetContentAndHeaders">{{menuFirst}}</a></li>
                <li><a href="#portfolio" @click="togglePortfolioVisible">{{menuSecond}}</a></li>
                <li><a href="#contacts" @click="toggleContactsVisible">{{menuThird}}</a></li>
              </ul>
            </div>
          </div>
        </nav>
      </div>
    </div>
</template>

<<script>
    
    import axios from 'axios';

    export default {
        data(){
            return {
                companyName: "",
                menuFirst: "",
                menuSecond:"",
                menuThird:""
            }
        },
        created(){
            axios.get('src/assets/data/navbar.json')
                .then(response => {
                    this.companyName = response.data.companyName;
                    this.menuFirst = response.data.menuFirst;
                    this.menuSecond = response.data.menuSecond;
                    this.menuThird = response.data.menuThird;
                })
                .catch(e => {
                    console.log('error');
                })
        }
    }
</script>