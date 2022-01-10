<template>
  <q-card>
    <q-item>
      <q-item-section avatar>
        <q-avatar>
          <img src="~assets/avatar2.jpeg">
        </q-avatar>
      </q-item-section>

      <q-item-section>
        <q-item-label>{{girl.name}}</q-item-label>
        <!--<q-item-label caption>Subhead</q-item-label>-->
      </q-item-section>
    </q-item>

    <q-card-section>
      <div class="text-subtitle2">Loves</div>
      <q-list>
        <q-item v-for="item in girl.lovesItems" :key="item.id">
          <q-item-section>{{item.item.name}} {{item.degree}}</q-item-section>
        </q-item>
      </q-list>
    </q-card-section>

    <q-separator />

    <q-card-section>
      <div class="text-subtitle2">Likes</div>
      <q-list>
        <q-item v-for="item in girl.likesItems" :key="item.id">
          <q-item-section>{{item.item.name}} {{item.degree}}</q-item-section>
        </q-item>
      </q-list>
    </q-card-section>
  </q-card>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'GirlItems',
  props: {
    girl: {
      type: Object,
      required: true
    }
  }
})
</script>
