<script setup lang="ts">
import { ref } from 'vue';

const leftDrawerOpen = ref(false);

const toggleMenu = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value;
};

const menuList = [
  {
    icon: 'home',
    label: 'Home',
    separator: false,
    path: '/home',
  },
  {
    icon: 'person',
    label: 'User',
    separator: false,
    path: '/player',
  },
  {
    icon: 'star',
    label: 'FNM',
    separator: false,
    path: '/fnm',
  },
];
</script>

<template>
  <q-layout view="hHh lpR fFf">
    <q-drawer
      v-model="leftDrawerOpen"
      side="left"
      show-if-above
      :width="200"
      :breakpoint="500"
      bordered
      class="bg-grey-3"
    >
      <q-scroll-area class="fit">
        <q-list>
          <template v-for="(menuItem, index) in menuList" :key="index">
            <q-item clickable :to="menuItem.path" v-ripple>
              <q-item-section avatar>
                <q-icon :name="menuItem.icon" />
              </q-item-section>
              <q-item-section>
                {{ menuItem.label }}
              </q-item-section>
            </q-item>
            <q-separator :key="'sep' + index" v-if="menuItem.separator" />
          </template>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <div class="absolute" style="top: 8px; z-index: 9999">
        <q-btn
          dense
          round
          unelevated
          color="grey-8"
          :icon="leftDrawerOpen ? 'chevron_left' : 'chevron_right'"
          @click="toggleMenu"
        />
      </div>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
