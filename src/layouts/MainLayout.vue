<template>
  <q-layout view="lHh Lpr fff">
    <q-header elevated height-hint="64">
      <q-toolbar class="ML__toolbar" style="height: 64px">
        <!--
        <q-btn
          flat
          dense
          round
          aria-label="Menu"
          icon="menu"
          class="q-mx-md"
        />
        -->

        <q-toolbar-title v-if="$q.screen.gt.sm" shrink class="row items-center no-wrap">
          <span>DOAX3 Girls</span>
        </q-toolbar-title>

        <q-space />

        <search-box class="col q-mx-md ML__toolbar-input" :items="seachItems" @on-select="select($event)"/>

        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn round dense flat :icon="$q.dark.isActive ? 'light_mode' : 'dark_mode'" @click="$q.dark.toggle()">
            <q-tooltip>Toggle Dark Mode</q-tooltip>
          </q-btn>
        </div>

      </q-toolbar>
    </q-header>

    <q-page-container class="ML__page-container">
      {{item}}
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import SearchBox from 'src/components/SearchBox.vue'
import { itemsList } from 'src/components/items'
import { girlsList } from 'src/components/girls'

export default {
  components: { SearchBox },
  name: 'MainLayout',

  setup () {
    const router = useRouter()
    const search = ref('')

    const seachItems = [
      ...girlsList.map(x => ({ type: 'girl', name: x.name, value: `girl:${x.name}`, data: x })),
      ...itemsList.map(x => ({ type: 'item', name: x.name, value: `item:${x.name}`, data: x }))
    ]

    const select = (item) => {
      const id = item || undefined
      router.push({ name: 'index', query: { id } })
    }

    return {
      search,
      seachItems,
      select,
      item: ref(null)
    }
  }
}
</script>

<style lang="sass">
.ML

  &__toolbar
    height: 64px

  &__toolbar-input
    max-width: 40rem !important

  @media (min-width: 1024px)
    &__page-container
      padding-left: 94px
</style>
