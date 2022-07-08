<script setup>
import { ref, reactive, provide, computed } from 'vue';
import data from '@/db/stays.json';

import Header from './components/Header.vue';
import Card from './components/Item_card.vue';
import Modal from './components/Modal.vue';
import FullSearch from './components/FullSearch.vue';

const stays = data;
const modalVisible = ref(false);
const searchOption = reactive({
  location: null,
  guests: null
});

function toggleModal() {
  modalVisible.value = !modalVisible.value; 
}
function setsearchOption(value) {
  searchOption.location = value[0];
  searchOption.guests = value[1];
  toggleModal();
}

provide('visible', {
  modalVisible,
  toggleModal
});


const filteredStays = computed(() => {
  return stays.filter((item) => {
    if(searchOption.location == null && searchOption.guests == null) return item;
    let locationStringSplited = searchOption.location.split(', ');
    let city = locationStringSplited[0];
    let country = locationStringSplited[1];

    if(item.city == city && item.country == country && item.maxGuests >= searchOption.guests) return item;
  })
})

</script>

<template>
  <Header :location=searchOption.location :guestNum=searchOption.guests />
  <main class="container">
    <header class="main-content-header">
      <h1>Stays in Finland</h1>
      <p>{{ filteredStays.length }} stays</p>
    </header>
    <section class="item-list">
      <Card v-for="item in filteredStays" :key="item.title" :stay=item />
    </section>
  </main>

  <Modal>
    <FullSearch :location=searchOption.location :guestNum=searchOption.guests @action="setsearchOption" />
  </Modal>


  <footer>
    created by <strong>Whenz91</strong> - devChallenges.io
  </footer>
</template>

<style>
@import './assets/base.css';

.main-content-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 32px;
}
.item-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 49px 32px;
}
.container {
  width: 90%;
  margin: 0 auto;
}

@media screen and (max-width: 500px) {
    .item-list {
      grid-template-columns: 1fr;
    }
}
</style>
