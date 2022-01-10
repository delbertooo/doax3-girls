<template>
  <q-card>
    <q-item>
      <q-item-section avatar>
        <q-avatar color="secondary" icon="category" />
      </q-item-section>

      <q-item-section>
        <q-item-label>{{item.name}}</q-item-label>
        <!--<q-item-label caption>Subhead</q-item-label>-->
      </q-item-section>
    </q-item>

    <q-card-section v-if="girlsLove.length">
      <div class="text-subtitle2">Girls loving this</div>
      <q-list>
        <q-item v-for="girl in girlsLove" :key="girl.id">
          <q-item-section>{{girl.name}}</q-item-section>
        </q-item>
      </q-list>
    </q-card-section>

    <q-separator v-if="girlsLove.length" />

    <q-card-section v-if="girlsLike.length">
      <div class="text-subtitle2">Girls liking this</div>
      <q-list>
        <q-item v-for="girl in girlsLike" :key="girl.id">
          <q-item-section>{{girl.name}}</q-item-section>
        </q-item>
      </q-list>
    </q-card-section>
  </q-card>
</template>

<script>
import { defineComponent, watch, ref } from 'vue'
import { girlsList } from './girls'

export default defineComponent({
  name: 'ItemGirls',
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  setup (props) {
    const girlsLove = ref([])
    const girlsLike = ref([])

    watch(
      () => props.item,
      newItem => {
        girlsLove.value = girlsList.filter(x => x.lovesItems.some(i => i.item.id === newItem.id))
        girlsLike.value = girlsList.filter(x => x.likesItems.some(i => i.item.id === newItem.id))
      },
      { immediate: true }
    )
    return {
      girlsLove,
      girlsLike
    }
  }
})
</script>
