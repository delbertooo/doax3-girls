<template>
  <q-page class="flex flex-center">
    <div class="q-my-md">
      <girl-items v-if="type === 'girl'" :girl="it"/>
      <item-girls v-else-if="type === 'item'" :item="it"/>
    </div>
  </q-page>
</template>

<script>
import GirlItems from 'src/components/GirlItems.vue'
import ItemGirls from 'src/components/ItemGirls.vue'
import { defineComponent, ref, watch } from 'vue'
import { useRoute } from 'vue-router'
import { item } from 'src/components/items'
import { girl } from 'src/components/girls'

export default defineComponent({
  components: { GirlItems, ItemGirls },
  name: 'PageIndex',
  setup () {
    const route = useRoute()
    const type = ref(null)
    const it = ref(null)

    watch(
      () => route.query.id,
      newId => {
        const matches = /^([^:]+):(.+)$/.exec(newId || '') || []
        const t = matches[1]
        const id = matches[2]
        if (t === 'girl') {
          type.value = t
          it.value = girl(id)
        } else if (t === 'item') {
          type.value = t
          it.value = item(id)
        } else {
          type.value = null
          it.value = null
        }
      },
      { immediate: true }
    )

    return {
      type,
      it
    }
  }
})
</script>
