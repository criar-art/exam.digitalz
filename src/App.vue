<script setup>
import { ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
const drawer = ref(false)
</script>

<template>
    <!-- <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div> -->
    <v-layout>
      <v-app-bar
        color="primary"
        prominent
      >
        <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

        <v-toolbar-title>My exam</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn variant="text" icon="mdi-magnify"></v-btn>

        <v-btn variant="text" icon="mdi-filter"></v-btn>

        <v-btn variant="text" icon="mdi-dots-vertical"></v-btn>
      </v-app-bar>

      <v-main style="height: 500px;">
        <v-card-text>
          <RouterView />
        </v-card-text>
      </v-main>
    </v-layout>
</template>

<style>
* {
  color: #000;
}
</style>