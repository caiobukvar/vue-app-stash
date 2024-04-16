<script setup lang="ts">
import StashWelcome from './components/StashWelcome.vue'
import IPTrackerView from './views/IPTrackerView.vue'
import CurrencyConverterView from './views/CurrencyConverterView.vue'
import AlarmsView from './views/AlarmsView.vue'
import TranslatorView from './views/TranslatorView.vue'
import WeatherView from './views/WeatherView.vue'
import { ref } from 'vue'

const showAppDetails = ref(false)
const selectedApp = ref('')

function changeAppDetails(e: MouseEvent) {
  showAppDetails.value = true
  selectedApp.value = (e.target as HTMLInputElement).name
}
</script>

<template>
  <header>
    <!-- logo vite + logo BKVR, inline -->
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <StashWelcome msg="Welcome to Bukvar's Vue App stash!" />

      <div class="btn-container">
        <!-- ao clicar abrir na direita o app selecionado -->
        <!-- adicionar tooltip com descrição de cada app on hover -->
        <button class="details-btn" @click="(e) => changeAppDetails(e)" name="alarmous">
          Alarmous
        </button>
        <button class="details-btn" @click="(e) => changeAppDetails(e)" name="ip-tracker">
          IPTracker
        </button>
        <button class="details-btn" @click="(e) => changeAppDetails(e)" name="currency-converter">
          Currency Converter
        </button>
        <button class="details-btn" @click="(e) => changeAppDetails(e)" name="translator">
          Translator
        </button>
        <button class="details-btn" @click="(e) => changeAppDetails(e)" name="weather">
          How's the weather?
        </button>
      </div>
    </div>
  </header>

  <main>
    <!-- tudo aqui dentro sera um preview de cada app, renderizado on hover -->
    <div v-if="showAppDetails">
      <AlarmsView v-show="selectedApp === 'alarmous'" />
      <IPTrackerView v-show="selectedApp === 'ip-tracker'" />
      <CurrencyConverterView v-show="selectedApp === 'currency-converter'" />
      <TranslatorView v-show="selectedApp === 'translator'" />
      <WeatherView v-show="selectedApp === 'weather'" />
    </div>

    <div v-else>
      <h1>Please, select an app to see details.</h1>
    </div>
  </main>

  <button class="floating-btn">?</button>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

main {
  background-color: rgba(37, 48, 43, 0.288);
  padding: 10px;
  border-radius: 6px;
  box-shadow: 0 0 5px 2px rgba(0, 189, 126, 0.5);
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.floating-btn {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 48px;
  height: 48px;
  cursor: pointer;
}

.floating-btn:hover {
  scale: 1.1;
}

.btn-container {
  display: flex;
  gap: 10px;
}

.details-btn {
  background-color: rgba(0, 189, 126, 1);
  border: none;
  border-radius: 6px;
  padding: 4px;
  height: 32px;
  cursor: pointer;
}

.details-btn:hover {
  scale: 1.05;
  background-color: rgba(0, 189, 126, 0.75);
}

@media (min-width: 1024px) {
  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
