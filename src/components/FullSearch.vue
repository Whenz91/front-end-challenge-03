<script setup>
import { inject, ref, watch } from 'vue'
const {modalVisible, toggleModal} =  inject('visible');
const props = defineProps({
    location: String,
    guestNum: Number
})


const text = ref(props.location);
const allGuests = ref(props.guestNum);
const locationInput = ref(false);
const guestsInput = ref(false);
const adults = ref(0);
const children = ref(0);

const emit = defineEmits(['action'])
const action = () => emit('action', [text, allGuests]);

const locationList = [
  'Helsinki, Finland',
  'Turku, Finland',
  'Oulu, Finland',
  'Vaasa, Finland'
];

const closeAll = () => {
   locationInput.value = false;
  guestsInput.value = false;
}
const locationInputClick = () => {
  locationInput.value = true;
  guestsInput.value = false;
}
const gusetInputClick = () => {
  guestsInput.value = true;
  locationInput.value = false;
}

watch(
  () => adults.value + children.value,
  (sum) => {
    allGuests.value = sum;
  }
)

</script>

<template>
  <div class="search-outer" @click="closeAll">

    <header class="mobile-header">
      <p>Edit your search</p>
      <button class="close-btn">
        <span class="material-icons-outlined" @click="toggleModal">
          close
        </span>
      </button>
    </header>

    <div class="search-wrapper" @click.stop>
      <div class="input-group" @click="locationInputClick">
          <label for="location">Location</label>
          <input 
            id="location" 
            type="text" 
            placeholder="Location" 
            v-model="text" 
          >
      </div>
      <div class="input-group" @click="gusetInputClick">
          <label for="guests">Guests</label>
          <input 
            id="guests" 
            type="number" 
            placeholder="Add guests"
            v-model="allGuests"
          >
      </div>
      <button class="search-btn" @click="action">
        <span class="search-icon material-icons-outlined">
          search
        </span>
        Search
      </button>
    </div>

    <div class="input-plus-info-wrapper" @click.stop>

      <ul class="option-list" v-if="locationInput">
        <li v-for="item in locationList" :key="item" @click="text = item">
          <span class="material-icons-outlined">place</span>
          {{ item }}
        </li>
      </ul>

      <div class="guest-controll-wrapper" v-if="guestsInput">

        <div class="guest-controll-group">
          <label for="adult">
            Adults
            <span>Ages 13 or above</span>
          </label>
          <div class="input-with-buttons">
            <button @click="adults != 0 ? adults-- : ''">-</button>
            <input type="number" id="adult" v-model="adults">
            <button @click="adults++">+</button>
          </div>
        </div>

        <div class="guest-controll-group">
          <label for="children">
            Children
            <span>Ages 2-12</span>
          </label>
          <div class="input-with-buttons">
            <button @click="children != 0 ? children-- : ''">-</button>
            <input type="number" id="children" v-model="children">
            <button @click="children++">+</button>
          </div>
        </div>

      </div>

    </div>

  </div>

</template>

<style scoped>
.search-outer {
  width: 100%;
  height: 100%;
  padding: 93px 97px;
  position: relative;
}

.mobile-header {
  display: none;
}
.mobile-header p {
  font-weight: 700;
  font-size: 12px;
  line-height: 15px;
}
.close-btn {
  border: none;
  background: transparent;
  cursor: pointer;
}

.search-wrapper {
  display: flex;
  box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  overflow: hidden;
}
.input-group {
    flex-grow: 2;
    max-width: 426px;
    padding: 12px 26px;
    border: 1px solid transparent;
    border-right: 1px solid var(--c-gray-2);
    border-radius: 16px;
}
.input-group > label {
    text-transform: uppercase;
    font-weight: 800;
    font-size: 9px;
    line-height: 11px;
}
.input-group > input {
    width: 100%;
    display: block;
    border: none;
    padding: 4px 0;
    outline: none;
    font-family: var(--ff-mulish);
    font-weight: 400;
    font-size: 14px;
}
.input-group:focus-within {
    border: 1px solid rgba(51, 51, 51, 1);
}

.search-btn {
    display: flex;
    align-items: center;
    column-gap: 10px;
    border-radius: 16px;
    padding: 15px 27px;
    margin: 0 auto;
    background-color: var(--c-red);
    color: var(--c-white);
    border: none;
    cursor: pointer;
}
.search-icon {
  color: var(--c-white);
}

.input-plus-info-wrapper {
  display: grid;
  grid-template-columns: repeat(3, 40%);
  grid-template-areas: 
  "locationBox gusetBox ."
  ;
}

.option-list {
  grid-area: locationBox;
  list-style: none;
  margin: 41px 0 0;
}
.option-list > li {
  display: flex;
  align-items: center;
  column-gap: 10px;
  margin-bottom: 34px;
  cursor: pointer;
}

.guest-controll-wrapper {
  grid-area: gusetBox;
  margin-top: 48px;
}

.guest-controll-group label {
  display: block;
  margin-bottom: 12px;
  font-weight: 700;
  font-size: 14px;
  line-height: 18px;
}
.guest-controll-group label span {
  display: block;
  font-weight: 500;
  color: var(--c-gray-1);
}

.input-with-buttons {
  margin-bottom: 52px;
}
.input-with-buttons > input {
  width: 70px;
  text-align: center;
  padding: 0 15px;
  border: none;
}
.input-with-buttons > input::-webkit-outer-spin-button,
.input-with-buttons > input::-webkit-inner-spin-button {
 -webkit-appearance: none;
  margin: 0;
}
.input-with-buttons > button {
  border: 1px solid var(--c-gray-3);
  color: var(--c-gray-3);
  background-color: transparent;
  width: 23px;
  height: 23px;
  border-radius: 4px;
}

@media screen and (max-width: 500px) {
  .search-outer {
    padding: 18px 21px;
  }
  .mobile-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
  }
  .search-wrapper {
    flex-direction: column;
  }
  .search-btn {
    position: absolute;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%);
  }
  .input-group {
    border-right: none;
    border-bottom: 1px solid var(--c-gray-2);
    
  }
  .input-plus-info-wrapper {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-areas: 
    "locationBox"
    "gusetBox"
    ;
    justify-items: center;
  }
  .option-list {
    padding: 0;
  }
}

</style>