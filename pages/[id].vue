<script setup lang="ts">
import { LocalStorage} from 'quasar'
const route = useRoute();
const expanded = ref(true);

const {data} =  await useAsyncData('', () => $fetch('https://fakestoreapi.com/products')) || []

const multiple = ref(null)

const options = [
        'Google', 'Facebook', 'Twitter', 'Apple', 'Oracle'
      ]

const product = computed(() => {
  let product = data.value.filter(function (elem, i) {
    if (elem.id == route.params.id) return true;
    return false
  })

  LocalStorage.set(product[0].id, product[0]);

  return product
})



</script>
<template>


  <div class="q-pa-md row items-start q-gutter-md">
    <q-card class="my-card" flat bordered>
      

      <q-card-section>
        <div class="text-overline text-orange-9">Overline</div>
        <div class="text-h5 q-mt-sm q-mb-xs">{{ product[0].title }}</div>
        <div class="text-caption text-grey">
          {{ product[0].category }}
        </div>
      </q-card-section>

      <q-card-actions>
        <q-btn flat color="primary" label="Share" />
        <q-btn flat color="secondary" label="Book" />

        <q-space />

        <q-btn
          color="grey"
          round
          flat
          dense
          :icon="expanded ? 'keyboard_arrow_up' : 'keyboard_arrow_down'"
          @click="expanded = !expanded"
        />
      </q-card-actions>

      <q-slide-transition>
        <div v-show="expanded">
          <q-separator />
          <q-card-section class="text-subtitle2">
            {{ product[0].description }}
          </q-card-section>
        </div>
      </q-slide-transition>
      <q-img
        :src="product[0].image" 
      />
    </q-card>
  </div>
</template>