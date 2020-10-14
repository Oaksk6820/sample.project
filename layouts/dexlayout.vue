<template>
  <div>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-spacer />
      <H2> PokeDex Header </H2>
      <v-spacer />
    </v-app-bar>

    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </div>
</template>