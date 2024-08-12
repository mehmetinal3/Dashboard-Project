<template>
  <div :class="['body', { 'collapsed': isCollapsed }]">
    <Sidebar class="sidebar"
    :isCollapsed="isCollapsed"
      @update:isCollapsed="updateIsCollapsed"/>
    <div class="page-right">
      <Header />
      <ScreenField />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { useRouter } from 'vue-router';
import Header from '../components/Header.vue';
import Sidebar from '../components/Sidebar.vue';
import ScreenField from '../components/ScreenField.vue';
import '../assets/css/Screengrid/grid.css'

export default defineComponent({
  name: 'PageTwo',
  components: {
    Header,
    Sidebar,
    ScreenField,
  },
  setup() {
    const isCollapsed = ref(false);

    const updateIsCollapsed = (collapsed: boolean) => {
      isCollapsed.value = collapsed;
    };

    return {
      isCollapsed,
      updateIsCollapsed,
    };
  },
});
</script>

<style>
.body {
  /* display: flex;
  justify-content: center; */
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  color: #4a596a;
  background-color: #f3f7fa;
  display: grid;
  grid-template-columns: 270px 1fr;
  transition: grid-template-columns 0.8s ease;
}

.body.collapsed {
  display: grid;
  grid-template-columns: 130px 1fr;
}

@media (max-width: 800px) {
  .sidebar {
    display: none;
  }
  .body{
    grid-template-columns: 1fr;
  }
}

@media (max-width: 800px) {
  .row-1 .icon {
    display: none; /* 800px ve altında ikonları gizler */
  }
}
</style>