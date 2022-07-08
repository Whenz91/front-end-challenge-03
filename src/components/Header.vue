<script setup>
import { inject } from 'vue';
defineProps({
    location: String,
    guestNum: Number
})

const {modalVisible, toggleModal} =  inject('visible');

</script>

<template>
    <nav class="main-nav container">
        <a href="#" class="logo">
            <img src="@/assets/logo.svg" alt="windbnb">
        </a>

       <div class="search-wrapper" @click="toggleModal">
            <input class="search-input" type="text" placeholder="Location" :value="location">
            <input class="search-input" type="text" placeholder="Add guests" :value="guestNum">
            <button class="search-btn">
            <span class="search-icon material-icons-outlined">
                search
            </span>
            </button>
        </div>
    </nav>
</template>

<style scoped>
.main-nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 32px;
    padding-bottom: 64px;
}

.search-wrapper {
  display: flex;
  box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  overflow: hidden;
}
.search-input {
  border: none;
  border-right: 1px solid var(--c-gray-2);
  padding: 18px 16px;
  outline: none;
  font-family: var(--ff-mulish);
  font-weight: 400;
  font-size: 14px;
}
.search-btn {
  padding: 19px;
  background-color: transparent;
  border: none;
  cursor: pointer;
}
.search-icon {
  color: var(--c-red);
}


@media screen and (max-width: 500px) {
    .main-nav {
        flex-direction: column;
        row-gap: 39px;
    }
    .main-nav > :first-child {
        align-self: flex-start;
    }
    .main-nav > :last-child {
        align-self: center;
    }

    .search-input {
        max-width: 110px;
    }
}
</style>