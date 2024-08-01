<template>
  <v-responsive class="border rounded" max-height="300">
    <v-app>
      <v-app-bar :elevation="2" rounded>
        <template v-slot:prepend>
          <v-app-bar-nav-icon></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>Application Bar {{ username }} E-mail={{ email }}</v-app-bar-title>
        <div class="text-center">
          <v-btn
            append-icon="mdi-account-circle"
            prepend-icon="mdi-check-circle"
            @click="logOut"
          >
            <template v-slot:prepend>
              <v-icon color="success"></v-icon>
            </template>

            Logout

            <template v-slot:append>
              <v-icon color="warning"></v-icon>
            </template>
          </v-btn>
        </div>
      </v-app-bar>

      <v-navigation-drawer>
        <v-list>
          <v-list-item title="Navigation drawer"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-main>
        <v-container>
          <h1>Main Content</h1>
        </v-container>
      </v-main>
    </v-app>
  </v-responsive>
</template>
<script>
import axios from "axios"
export default {
  data:() => ({
    email:'',
    password: '',
    status: '',
    picture: '',
    username: ''
   }),
   
   async mounted() {
    let user = window.sessionStorage.getItem("email");
    console.log("user=", user);
    const response = await axios.get("http://localhost:7000/listid?email="+ user);
    let data = response.data;
    console.log('user=',data.row.username)
    this.email=data.row.email
    this.username=data.row.username


  },
  methods: {
    logOut() {
      window.sessionStorage.clear();
      this.$router.replace("/login");
    },
  },

};
</script>
