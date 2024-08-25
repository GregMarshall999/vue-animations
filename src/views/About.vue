<template>
    <div class="about">
        <transition 
            name="fade" 
            appear
            @before-enter="beforeEnter"
            @enter="enter"
            @after-enter="afterEnter"
            @before-leave="beforeLeave"
            @leave="leave"
            @after-leave="afterLeave">
            <h1 v-if="showTitle">A Propos</h1>
        </transition>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    </div>
</template>

<script setup> //alt click to select multiple lines like scroll click
import { ref } from 'vue';

const showTitle = ref(true);

const beforeEnter = e => { //add e after the leave hooks
    console.log('before enter', e);
};
const enter = e => {
    console.log('enter', e);
};
const afterEnter = e => {
    console.log('afterEnter', e);
    e.style.color = 'green';
    setTimeout(() => showTitle.value = false, 2000);
};

const beforeLeave = e => {
    console.log('before leave', e);
    e.style.color = 'pink';
};
const leave = e => {
    console.log('leave', e);
};
const afterLeave = e => {
    console.log('after leave', e);
};
</script>

<style>
.about {
    max-width: 600px;
    margin: 20px auto;
}

.fade-enter-from, .fade-leave-to {
    opacity: 0;
}
.fade-enter-active, .fade-leave-active {
    transition: opacity 3s ease;
}
</style>