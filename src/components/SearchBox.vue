<template>
  <q-select
    v-model="model"
    @update:modelValue="$emit('onSelect', $event)"
    :options="options"
    dense
    standout
    dark
    placeholder="Search girls or items"
    emit-value
    map-options

    fill-input
    hide-selected
    use-input
    input-debounce="0"
    @filter="filterFn"
  >
    <template v-slot:prepend>
      <q-icon v-if="model === null" name="search" />
      <q-icon v-else name="clear" class="cursor-pointer" @click="model = null; $emit('onSelect', null)" />
    </template>

    <template v-slot:no-option>
      <q-item>
        <q-item-section>
          No results
        </q-item-section>
      </q-item>
    </template>

    <template v-slot:option="scope">
      <q-item v-bind="scope.itemProps">
        <q-item-section avatar>
          <q-avatar v-if="scope.opt.icon == 'girl'">
            <img src="~assets/avatar2.jpeg">
          </q-avatar>
          <q-avatar color="secondary" v-else-if="scope.opt.icon" :icon="scope.opt.icon" />
          <q-avatar color="secondary" v-else icon="category" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ scope.opt.label }}</q-item-label>
        </q-item-section>
      </q-item>
    </template>
  </q-select>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'SearchBox',
  emits: ['onSelect'],
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  setup (props) {
    const fullOptions = props.items.map(x => ({
      label: x.name,
      value: x.value,
      icon: x.type === 'girl' ? 'girl' : undefined
    }))
    const options = ref(fullOptions)
    const model = ref(null)
    return {
      model,
      fullOptions,
      options,
      filterFn (val, update) {
        if (val === '') {
          update(() => {
            options.value = fullOptions
          })
          return
        }

        update(() => {
          const needle = val.toLowerCase()
          options.value = fullOptions.filter(v => v.label.toLowerCase().indexOf(needle) > -1)
        })
      }
    }
  }
})
</script>
