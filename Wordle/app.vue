<template>
  <NuxtLayout>
  
    <v-app>
      <v-app-bar color="primary" :elevation="2">
        <v-app-bar-title class="font"  @click="router.push('/')">
          Recycled Wordle
          <v-icon @click="router.push('/')">
            mdi-bookshelf
          </v-icon>
        </v-app-bar-title>
      </v-app-bar>

      <HelpDialog v-model="showHelpDialog" />

      <v-navigation-drawer expand-on-hover rail location="right" color="primary">
        <v-list>
          <v-list-item
          class="font"
            prepend-avatar="https://i.ibb.co/kx64H0R/Picture1.jpg"
            subtitle="CS Student"
            title="Cynthia"
          ></v-list-item>
        </v-list>

        <v-divider></v-divider>
        <v-list density="compact" nav>
          <v-list-item class="font"prepend-icon="mdi-home" title="home" @click="router.push('/')"/>
          <v-list-item  class="font"prepend-icon="mdi-cog-outline" title="settings" @click="settingsDialog = true"/>
          <v-list-item class="font" prepend-icon="mdi-help-circle" title="about" @click="router.push('/aboutPage')"/>
          <v-list-item class="font" prepend-icon="mdi-weather-night" title="dark mode"@click="toggleTheme()"/>
          <v-list-item class="font" prepend-icon="mdi-help" title="help!" @click="showHelpDialog = true" />
        </v-list>
      </v-navigation-drawer>
      
      <!-- Settings Dialog -->
      <v-dialog v-model="settingsDialog" max-width="250">
        <v-card style="" color="primary">
          <br>
          <p style="text-align: center; font-size: xx-large;" class="font"> Settings </p>
          <v-card-text>
            <v-container>
              <v-btn class="buttonClass font" @click="themeSettings('light')" elevation="8" tonal>Light Mode</v-btn>
              <v-btn class="buttonClass font" @click="themeSettings('dark')" elevation="8" tonal>Dark Mode</v-btn>
              <v-btn class="buttonClass font" @click="themeSettings('green')" elevation="8"tonal >green</v-btn>
              <v-btn class="buttonClass font" @click="themeSettings('greenDark')" elevation="8" tonal>green dark</v-btn>
              <v-btn class="buttonClass font" @click="themeSettings('tech')" elevation="8"tonal >tech</v-btn>
              <v-btn class="buttonClass font" @click="themeSettings('techDark')" elevation="8" tonal>tech dark</v-btn>
              <v-btn class="buttonClass font " @click="themeSettings('cozy')" elevation="8"tonal >cozy</v-btn>
              <v-btn class="buttonClass font" @click="themeSettings('cozyDark')" elevation="8" tonal>cozy dark</v-btn>
            </v-container>
          </v-card-text>
        </v-card>
      </v-dialog>

    
      <v-main>
        <NuxtPage />
      </v-main>

    </v-app>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { useTheme } from "vuetify";
import nuxtStorage from 'nuxt-storage';
import { ref } from "vue";

const router = useRouter();
const theme = useTheme();
const showHelpDialog = ref(false);
const settingsDialog = ref(false);
const wordEngineDialog = ref(false);

onMounted(() => {
  var defaultTheme = nuxtStorage.localStorage.getData("theme");
  theme.global.name.value = defaultTheme ?? "dark";
});

function toggleTheme() {
  theme.global.name.value = theme.global.name.value === "light" ? "dark" : "light";
  nuxtStorage.localStorage.setData("theme", theme.global.name.value);
}

function themeSettings(item: string) {
  theme.global.name.value = item;
  nuxtStorage.localStorage.setData("themes", theme.global.name.value);
}


</script>
<style>
.buttonClass{
  display: flex;
  justify-content: center;
  border: 2px;
  margin-bottom: 10px;
}

.font{
  font-family: 'Lucida Sans';
}
</style>