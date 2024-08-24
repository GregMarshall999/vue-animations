<template>
    <div class="home">
        <Toast v-if="showToast"/>
        <Todos @badValue="triggerToast"/>
    </div>
</template>

<script>
import Toast from '@/components/Toast.vue';
import Todos from '@/components/Todos.vue';
import { ref } from 'vue';

export default {
    components: { Toast, Todos }, 
    setup() {
        const showToast = ref(false);

        const triggerToast = () => {
            showToast.value = true;
            setTimeout(() => showToast.value = false, 3000);
        }

        return { showToast, triggerToast }
    }
}
</script>

<style>

.home {
    display: flex;
    justify-content: center;
}

</style>