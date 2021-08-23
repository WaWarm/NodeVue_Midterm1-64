<template>
  <div>
    <h1>Salad Ingredients</h1>
    <div v-if="users.length">
      <h4>order {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            create order
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
                
        <p>name: {{ user.name }} - {{ user.lastname }}</p>
        <p>Vegetabletype: {{ user.email }}</p>
        <p>cream: {{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            your order
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            edit
          </button>
          <button v-on:click="deleteUser(user)">
            delete
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>