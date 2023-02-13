<script setup>
// import ButtonCounter from './components/ButtonCounter.vue';
import { ref, computed, onMounted} from 'vue';

import LoadingSpinner from './components/LoadingSpinner.vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';


const posts = ref([]);
const postxpage = 5;
const inicio = ref(0);
const fin = ref(postxpage);
const loading = ref(true);

const favorite = ref("");

const changeFavorite = (title) => {
    favorite.value = title;
};

const next = () => {
    inicio.value +=  + postxpage;
    fin.value += + postxpage;
}

const prev = () => {
    inicio.value += - postxpage;
    fin.value += - postxpage;
};

// onMounted(async() => {
//     loading.value = true;
//     try {
//         const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//         posts.value = await res.json();
//     } catch (error) {
//         console.log(error)
//     } finally {
//         loading.value = false;
//     }
// })

fetch('https://jsonplaceholder.typicode.com/posts')
    .then(res => res.json())
    .then(data => {
        posts.value = data;
    })
    .finally(()=> loading.value = false)

</script>

<template>
    <LoadingSpinner v-if="loading"/>
    <div class="container" v-else>
        <h1 class="d-flex justify-content-center mt-2">APP de posts</h1>
        <h2 class="mb-3">Mis post favoritos: {{ favorite }}</h2>

        <PaginatePost 
            @next="next" 
            @prev="prev" 
            :inicio="inicio" 
            :fin="fin" 
            class="mb-2"
            :maxLength="posts.length"
        />
        <!-- <ButtonCounter />  -->
        <BlogPost 
            v-for="post in posts.slice(inicio, fin)" 
            :key="post.id" 
            :title="post.title" 
            :id="post.id" 
            :body="post.body" 
            :changeFavorite="changeFavorite"
        />
    </div>
</template>