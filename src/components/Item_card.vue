<script setup>
import Tag from './Tag.vue';
defineProps({
    stay: Object
})
</script>

<template>
  <article class="card">

        <img :src="stay.photo" :alt="stay.title" class="card-img">

        <div 
            :class="[
                'card-head',
                {'col-3': stay.superHost}
            ]"
        >
            <Tag v-if="stay.superHost">Super Host</Tag>

            <p class="secondary-text">{{stay.type}} {{stay.beds != null ? `. ${stay.beds} beds` : ''}}</p>
                
            <div class="rating">
                <span class="material-icons-outlined red-icon">
                    star
                </span>
                {{stay.rating}}
            </div>
        </div>

        <div class="card-main">
            {{ stay.title }}
        </div>

  </article>
</template>


<style scoped>
.card-img {
    width: 100%;
    height: auto;
    aspect-ratio: 6 / 4;
    object-fit: cover;
    border-radius: 24px;
}
.card-head {
    margin-top: 15px;
    display: grid;
    align-items: center;
    column-gap: 11px;
    grid-template-columns: 5fr 1fr;
}
.card-head.col-3 {
    grid-template-columns: 2fr 3fr 1fr;
}
.secondary-text {
    line-height: 17px;
    color: var(--c-gray-3);
}

.rating {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.red-icon {
    color: var(--c-red);
}

.card-main {
    margin-top: 17px;
    font-weight: 600;
    font-size: 16px;
    line-height: 20px;
}
</style>