<script setup>
import { ref } from 'vue'
import { RouterView } from 'vue-router'
const drawer = ref(false)
</script>

<template>
  <v-layout>
    <v-app-bar
      color="primary"
      prominent
    >
      <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer" />
      <v-toolbar-title>Exam-Digitalz</v-toolbar-title>
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
        <v-list-item prepend-icon="mdi-account" title="My Account" value="account" to="/about"></v-list-item>
        <!-- <v-list-item prepend-icon="mdi-account-group-outline" title="Users" value="users"></v-list-item> -->
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <v-card-text>
        <RouterView />
      </v-card-text>
    </v-main>
  </v-layout>
</template>
