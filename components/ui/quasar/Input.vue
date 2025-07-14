<script setup>
const props = defineProps({ invalid: Boolean, label: String, errorMessage: String, field: Object })
</script>
<template>
    <q-input type="text" counter minlength="3" maxlength="128" hint="" 
        :label="props.label"
        :aria-invalid="props.invalid" v-bind="field" :error-message="props.errorMessage"
        :error="!!props.errorMessage" />
</template>
