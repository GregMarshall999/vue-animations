<template>
    <div class="about">
        <transition 
            appear
            @before-enter="beforeEnter"
            @enter="enter"
            @after-enter="afterEnter"
        >
            <h1>A Propos</h1>
        </transition>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    </div>
</template>

<script setup>
//lien gsap: https://gsap.com/
import gsap from 'gsap';

const beforeEnter = e => {
    console.log('before enter - set initial state');
    e.style.transform = 'translateY(-60px)';
    e.style.opacity = 0;
};
const enter = (e, done) => {
    console.log('enter start - make transition');
    gsap.to(e, {
        duration: 1,
        y: 0,
        opacity: 1, 
        ease: 'bounce.out', 
        onComplete: done //add done after showing afterEnter
    });
};
const afterEnter = () => {
    console.log('after enter');
};

</script>

<style>
.about {
    max-width: 600px;
    margin: 20px auto;
}
</style>