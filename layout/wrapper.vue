<template>
  <q-layout view="hHh lpR fFf">

    <q-header reveal bordered class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          Title
        </q-toolbar-title>

        <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/page1" label="Page One" />
        <q-route-tab to="/page2" label="Page Two" />
        <q-route-tab to="/page3" label="Page Three" />
      </q-tabs>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" side="left" bordered>
       <div class="q-pa-md bg-grey-9 text-white">
    <q-list dark padding bordered class="rounded-borders" style="max-width: 328px">
      <q-expansion-item
        icon="perm_identity"
        label="Лояльность"
      >
        <q-card class="bg-grey-9">
          <q-card-section>
            Зарегистрируйтесь и получите скидку в 10%!
          </q-card-section>
        </q-card>
      </q-expansion-item>

      <q-expansion-item
        icon="signal_wifi_off"
        label="Доставка"
      >
        <q-card class="bg-grey-9">
          <q-card-section>
            Возможна аж до подъезда
          </q-card-section>
        </q-card>
      </q-expansion-item>

      <q-expansion-item
        icon="drafts"
        label="Партнерам"
        header-class="text-orange"
      >
        <q-card class="bg-grey-9">
          <q-card-section>
            Будете всегда ходить с улыбкой на лице, находясь в приятном шоке от нас!
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
    <NuxtLink to="/register"><LazyQBtn color="primary"  glossy label="Зарегистрироваться" ></LazyQBtn></NuxtLink>
  </div>   
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      
    </q-drawer>

    <q-page-container>
      <slot></slot>
      <q-page-scroller position="bottom-right" :scroll-offset="150" :offset="[18, 18]">
            <q-btn fab icon="keyboard_arrow_up" color="accent" />
          </q-page-scroller>
    </q-page-container>

    <q-footer reveal elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          <div>Title</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script setup>
import { ref } from 'vue'

    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

   
      
    const  toggleLeftDrawer  = function () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }

      
     const toggleRightDrawer = function () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      }
    

</script>