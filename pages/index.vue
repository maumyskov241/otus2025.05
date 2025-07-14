<script setup lang="ts">
import { NuxtLink } from '#components';
import { LocalStorage} from 'quasar'

const route = useRoute();

const {data} =  await useAsyncData('', () => $fetch('https://fakestoreapi.com/products'))


</script>
<template>

<div id="wrapper">   
<div class="q-pa-md row items-start q-gutter-md row">
    <q-card class="my-card"  flat bordered :key="product.id" v-for="product in data">
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

.q-card .text-caption {
  min-height:180px;
}

.q-card.my-card {
  width:30%;
}

.q-card .text-h5 {
  min-height: 65px;
}

html .bg-grey-9 {
    background-color : #a9a9a9!important;
}
</style>