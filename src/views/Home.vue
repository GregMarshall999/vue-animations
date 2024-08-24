<template>
    <div class="home">
        <Toast v-if="showToast"/>
        <Todos @badValue="triggerToast"/>

        <transition name="fade"> <!--on scope cette transition a fade-->
            <div v-if="showP">Salut, je suis une transition</div>
        </transition>

        <button @click="showP = !showP">{{ showP ? 'Cacher' : 'Afficher' }}</button>
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
        const showP = ref(false);

        const triggerToast = () => {
            showToast.value = true;
            setTimeout(() => showToast.value = false, 3000);
        }

        return { showToast, triggerToast, showP }
    }
}
</script>

<style>

.home {
    display: flex;
    flex-direction: column;
    justify-content: center;

    button {
        width: 100px;
        align-self: center;
    }
}

.fade-enter-from {
    opacity: 0;
}
.fade-enter-to {
    opacity: 1;
}
.fade-enter-active {
    /*transition: opacity 2s ease;*/
    transition: all 2s ease;
}

/* Vue peut autodetecter les valeurs par defaut et rendre les animations implicite
.fade-leave-from {
    opacity: 1;
}*/
.fade-leave-to {
    opacity: 0;
}
.fade-leave-active { /* on peut factoriser avec .fade-enter-active, .fade-leave-active {} */
    transition: all 2s ease;
}


</style>