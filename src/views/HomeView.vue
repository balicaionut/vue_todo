<template>
  <div class="home">
    <todoMain />
  </div>
</template>

<script>
import todoMain from '@/components/todoMain.vue';

export default {
  name: 'HomeView',
  components: {
    todoMain,
  },
};
</script>
