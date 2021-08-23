<template>
  <div>
    <h1>Show User</h1>
    
    <p>name {{ user.name }} - {{ user.lastname }}</p>
    <p>Vegetabletype: {{ user.email }}</p>
    <p>cream: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>