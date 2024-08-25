<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">A propos</router-link> | 
    <router-link to="/contact">Contact</router-link>
  </nav>
  <router-view v-slot="{ Component }">
    <transition :name="transitionName" mode="out-in">
      <component :is="Component"></component>
    </transition>
  </router-view>
</template>

<script setup>
import { computed, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const previousRoute = ref(route.fullPath);

const transitionName = computed(() => {
  //const routesOrder = ['/', '/about', '/contact'];
  //console.log(router.getRoutes().map(r => r.path));
  const routesOrder = router.getRoutes().map(r => r.path);

  const currentIndex = routesOrder.indexOf(route.path);
  const previousIndex = routesOrder.indexOf(previousRoute.value);

  previousRoute.value = router.currentRoute.value.fullPath;

  if(currentIndex < previousIndex) {
    return 'route-right';
  } 
  else {
    return 'route-left';
  }
});
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  background: #f2f2f2;
}

nav {
  padding: 30px;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}
nav a.router-link-exact-active {
  color: #42b983;
}

.route-left-enter-from {
  opacity: 0;
  transform: translateX(100px);
}
.route-left-leave-to {
  opacity: 0;
  transform: translateX(-100px);
}

.route-right-enter-from {
  opacity: 0;
  transform: translateX(-100px);
}
.route-right-leave-to {
  opacity: 0;
  transform: translateX(100px);
}

.route-left-enter-active, .route-right-enter-active {
  transition: all 0.3s ease-out;
}
.route-left-leave-active, .route-right-leave-active {
  transition: all 0.3s ease-in;
}
</style>
