<template>
    <div class="q-pa-lg">
        <q-range class="q-mt-xl" v-model="range" color="deep-orange" label-always :max="50" track-size="8px" track-color="grey-2"
            inner-track-color="transparent"  :track-img="img" />
            <div class="q-field__label no-pointer-events ellipsis">Отрегулируйте диапазон цен</div>
    </div>
</template>

<script setup>
const img = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAH0lEQVQoU2NkYGAwZkAFZ5G5jPRRgOYEVDeB3EBjBQBOZwTVugIGyAAAAABJRU5ErkJggg=='

const props = defineProps({ name: String, range : Object, onChange : Function});
const range = ref(props.range);
watch(range, (newRange) => {
   props.onChange(props.name, newRange)
});
</script>
