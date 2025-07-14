<template>
  <div class="q-pa-md">
    <q-select filled label="Выберите категории товаров" hint="разделитель [,;|]" v-model="model" use-input use-chips
      multiple input-debounce="0" @new-value="createValue" :options="filterOptions" @filter="filterFn"
      style="width: 350px" />
  </div>{{ model }}
</template>

<script setup>

const props = defineProps({ name: String, model: Array, onChange: Function });
const model = ref(props.model);

watch(model, (newModel) => {
  props.onChange(props.name, newModel)
});

const stringOptions = [{ value: 0, label: "men's clothing" }, { value: 1, label: "jewelery" }, { value: 2, label: "electronics" }, { value: 3, label: "women's clothing" }]
const filterOptions = ref(stringOptions)
const createValue = function (val, done) {
  // Calling done(var) when new-value-mode is not set or is "add", or done(var, "add") adds "var" content to the model
  // and it resets the input textbox to empty string
  // ----
  // Calling done(var) when new-value-mode is "add-unique", or done(var, "add-unique") adds "var" content to the model
  // only if is not already set and it resets the input textbox to empty string
  // ----
  // Calling done(var) when new-value-mode is "toggle", or done(var, "toggle") toggles the model with "var" content
  // (adds to model if not already in the model, removes from model if already has it)
  // and it resets the input textbox to empty string
  // ----
  // If "var" content is undefined/null, then it doesn't tampers with the model
  // and only resets the input textbox to empty string

  if (val.length > 0) {
    const modelValue = (model.value || []).slice()

    val
      .split(/[,;|]+/)
      .map(v => v.trim())
      .filter(v => v.length > 0)
      .forEach(v => {
        if (stringOptions.includes(v) === false) {
          stringOptions.push(v)
        }
        if (modelValue.includes(v) === false) {
          modelValue.push(v)
        }
      })

    done(null)
    model.value = modelValue
  }
}

const filterFn = function (val, update) {
  update(() => {
    if (val === '') {
      filterOptions.value = stringOptions
    }
    else {
      const needle = val.toLowerCase()
      filterOptions.value = stringOptions.filter(
        v => v.label.toLowerCase().indexOf(needle) > -1
      )
    }
  })
}
</script>
