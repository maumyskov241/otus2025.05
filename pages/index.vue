<script setup lang="ts">
import { NuxtLink } from '#components';
import { LocalStorage} from 'quasar'

const route = useRoute();

const {data} =  await useAsyncData('', () => $fetch('https://fakestoreapi.com/products'))


</script>
<template>

<div id="wrapper">
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
<div class="q-pa-md row items-start q-gutter-md" style="flex-wrap: inherit">
    <q-card class="my-card" flat bordered :key="product.id" v-for="product in data">
      <q-card-section >
        <q-card-section class="q-pt-xs">
          <div class="text-overline">{{product.category}}</div>
          <div class="text-h5 q-mt-sm q-mb-xs">{{product.title}}</div>
          <div class="text-caption text-grey">
            {{product.description}}
          </div>
        </q-card-section>

        <q-card-section class="col-5 flex flex-center">
          <q-img
            class="rounded-borders"
            :src="product.image" width="200px" height="150px"
          />
        </q-card-section>
      </q-card-section>

      <q-separator />

      <q-card-actions>
        <q-btn flat round icon="money" />
        <q-btn flat>
          {{ product.price }} руб.
        </q-btn>
        <q-btn flat color="primary">
          <NuxtLink :to="{ name: 'id', params: { id: product.id }}"><LazyQBtn color="amber"  glossy label="Подробнее" ></LazyQBtn></NuxtLink>
        </q-btn>
      </q-card-actions>
    </q-card>
    </div>
    </div>
</template>
<style scoped>
#wrapper {
    display: flex;
   
}

html .bg-grey-9 {
    background-color : #a9a9a9!important;
}
</style>