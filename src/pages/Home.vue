<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">

        <!-- errors -->
        <div class="error" v-if="error">
          <p>{{ error }}</p>
        </div>


        <Search
          @search="search = $event"
          :value="search"
          placeholder="Type user name..."/>
        <button @click="getRepos" class="btn btnPrimary">Search!</button>


        <!-- wrapper -->
        <div class="repos__wrapper" v-if="repos">
          <!-- item -->
            <div class="repos__item" v-for="repo in repos" :key="repo.id">
                <div class="repos__info">
                    <a class="repo__link link" target="_blank" :href="repo.html_url">{{ repo.name }}</a>  
                    <span>{{ repo.stargazers_count}} ⭐</span>
                </div>
            </div>
        </div>
         <p class="noRep">{{ noRep }}</p>
      </div>
    </section>
  </div>
</template>

<script>
import  Search from '@/components/Search.vue'
import axios from 'axios'

export default {
  components:{
    Search
  },
  data() {
    return {
      search: '',
      error: null,
      repos: null,
      noRep: null
    }
  },
  methods: {
    getRepos() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then(answer => {
          if(answer.data.length == 0) {
            this.repos = null
            this.noRep = 'Users repositories are empty'
            console.log('gg');
          }else {
            this.noRep = null
            this.error = null
            this.repos = answer.data
          }

        })
        .catch(err => {
          this.noRep = null
          this.repos = null
          this.error = 'Cant find this user'  
        })
    }
  }
};
</script>

<style lang="scss" scoped>

.container {
  display: flex;
  align-items: center;
  flex-direction: column;
}
button {
  margin-top: 40px;
}


.repos__wrapper {
  max-width: 600px;
  width: 100%;
  margin: 30px 0;
}
.repos__info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 10px 0;
  border-bottom: 1px solid grey;
}

.error {
  margin-bottom: 20px;
  color: red;
  font-family: arial;
}
.noRep {
  margin-top: 20px;
  text-transform: uppercase;
  color: red;
}

</style>