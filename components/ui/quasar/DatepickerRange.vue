<template>
    <div class="q-pa-md">
        <div class="q-pb-sm"></div>

        <q-date v-model="ranges" range multiple  />
    </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({ name: String, ranges : Array, onChange : Function});
const ranges = ref(props.ranges);

watch(ranges, (newRanges) => {
   props.onChange(props.name, newRanges)
});
</script>
