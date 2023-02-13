<script setup>
// defineProps(["title", "id", "body"]);
defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: "sin descripcion"
    }, 
    changeFavorite: Function,
})

// const emit = defineEmits(['changeFavoriteName'])
//usar emit locales apra poder hacer uso de emit
</script>

<template>
    <div class="card mb-2">
        <div class="card-body">
            <h5 class="card-title"> {{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button 
            @click="changeFavorite(title)" 
            class="btn btn-outline-primary">
            Favorito</button>
        </div>
    </div>
</template>