<template>
    <div class="contact">
        <h1>Contact</h1>
        <!--intentionnaly put groupe for error fixing-->
        <transition-group 
            tag="ul"
            appear
            @before-enter="beforeEnter"
            @enter="enter"
        >
            <!--Add index when delay doesn't work-->
            <li v-for="(icon, index) in icons" :key="icon.name" :data-index="index">
                <span class="material-icons">{{ icon.name }}</span>
                <div>{{ icon.text }}</div>
            </li>
        </transition-group>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import gsap from 'gsap';

const icons = ref([
    { name: 'alternate_email', text: 'par email'},
    { name: 'local_phone', text: 'par telephone'},
    { name: 'local_post_office', text: 'par poste'},
    { name: 'local_fire_department', text: 'par signaux de fumée'},
]);

const beforeEnter = e => {
    e.style.opacity = 0;
    e.style.transform = 'translateY(100px)';
};
const enter = (e, done) => {
    gsap.to(e, {
        opacity: 1, 
        y: 0, 
        duration: 0.8, 
        onComplete: done, 
        //delay: 0.2  show delay before using index
        delay: e.dataset.index * 0.2
    });
};
</script>

<style>
.contact ul {
    padding: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    max-width: 400px;
    margin: 60px auto;
}

.contact li {
    list-style-type: none;
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    line-height: 1.5em;
}
</style>