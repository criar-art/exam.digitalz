<script setup>
import { ref } from 'vue'
import { RouterView } from 'vue-router'
const drawer = ref(false)

// import { initializeApp } from "firebase/app";
// import { getAuth } from "firebase/auth";

// TODO: Replace the following with your app's Firebase project configuration
// See: https://firebase.google.com/docs/web/learn-more#config-object
const firebaseConfig = {
  // ...
};

// Initialize Firebase
// const app = initializeApp(firebaseConfig);


// Initialize Firebase Authentication and get a reference to the service
// const auth = getAuth(app);

// console.log(auth)
</script>

<template>
  <v-layout>
    <v-app-bar
      color="primary"
      prominent
    >
      <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer" />
      <v-toolbar-title>Exam Digitalz</v-toolbar-title>
      <v-spacer></v-spacer>
      <!-- <v-btn variant="text" icon="mdi-magnify"></v-btn>
      <v-btn variant="text" icon="mdi-filter"></v-btn>
      <v-btn variant="text" icon="mdi-dots-vertical"></v-btn> -->
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      location="left"
      temporary
    >
      <v-list density="compact" nav>
        <v-list-item prepend-icon="mdi-home-city" title="Home" value="home" to="/"></v-list-item>
        <v-list-item prepend-icon="mdi-login" title="Login" value="login" to="/login"></v-list-item>
        <v-list-item prepend-icon="mdi-information" title="About" value="about" to="/about"></v-list-item>
        <!-- <v-list-item prepend-icon="mdi-account-group-outline" title="Users" value="users"></v-list-item> -->
      </v-list>
    </v-navigation-drawer>
    <v-main class="ma-10">
      <RouterView />
    </v-main>
    <v-footer app class="d-flex flex-column">
      <div class="px-4 py-2 bg-black text-center w-100">
        {{ new Date().getFullYear() }} — <strong>Exam Digitalz</strong>
      </div>
    </v-footer>
  </v-layout>
</template>
