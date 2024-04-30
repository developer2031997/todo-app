<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          TODO APP
        </q-toolbar-title>

        <div>{{ formattedString }}</div>

      </q-toolbar>
      <q-img
        src="https://media.istockphoto.com/id/920377882/photo/beautiful-landscape-with-high-mountains-with-illuminated-peaks-stones-in-mountain-lake.jpg?s=1024x1024&w=is&k=20&c=ey5LfCMRjRiutyQdRsAZZnFj4-RvJ11aGEfXx8y6YU8="
        class="header-img absolute-top" />

    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above :width="200" :breakpoint="600">
      <q-scroll-area style="height: calc(100% - 150px); margin-top: 150px; border-right: 1px solid #ddd">
        <q-list padding>
          <q-item v-for="links in linksList" :key="links.title" clickable v-ripple :to="`/${links.path}`">
            <q-item-section avatar>
              <q-icon :name="links.icon" />
            </q-item-section>

            <q-item-section>
              {{ links.title }}
            </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top"
        src="https://media.istockphoto.com/id/920377882/photo/beautiful-landscape-with-high-mountains-with-illuminated-peaks-stones-in-mountain-lake.jpg?s=1024x1024&w=is&k=20&c=ey5LfCMRjRiutyQdRsAZZnFj4-RvJ11aGEfXx8y6YU8="
        style="height: 150px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png">
          </q-avatar>
          <div class="text-weight-bold">Akshay Dhivare</div>
          <div>@akshay_dhivare</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container keep-alive>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import { date } from 'quasar'


defineOptions({
  name: 'MainLayout'
})

const linksList = [
  {
    title: 'Todo',
    icon: 'list',
    path: ''
  },
  {
    title: 'Help',
    icon: 'help',
    path: 'help'
  }
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}



const timeStamp = Date.now();
const formattedString = date.formatDate(timeStamp, 'YYYY - Do - MMMM');

</script>

<style>
.header-img {
  z-index: -1;
  height: 50px;

}
</style>