<template>
  <div class="q-pa-md" style="max-width: 400px">
    <div class="q-gutter-md">
      <q-badge color="secondary">№ карты: {{ model }}</q-badge>
      <q-input
        filled
        v-model="model"
        label="№ карты"
        mask="#### - #### - #### - ####"
        fill-mask="#"
        unmasked-value
        hint="Mask: #### - #### - #### - ####, FillMask: #"
      />
    </div>
  </div>
</template>

<script setup>

const props = defineProps({ name: String, model : String, onChange : Function});
const model = ref(props.model);

watch(model, (newModel) => {
   props.onChange(props.name, newModel)
});
</script>