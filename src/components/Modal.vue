<script setup>
import { ref, inject } from 'vue';

const {modalVisible, toggleModal} =  inject('visible');

</script>

<template>
    <teleport to="body">
        <div class="modal" @click="toggleModal()"  v-if="modalVisible">
            <div class="modal-content" @click.stop>
                <slot></slot>
            </div>
        </div>
    </teleport>
</template>


<style scoped>
    .modal {
        width: 100%;
        height: 100%;
        background-color: rgba(79, 79, 79, 0.4);
        position: absolute;
        inset: 0;
        z-index: 999;
    }
    .modal-content {
        background-color: var(--c-white);
        height: 460px;
    }
    @media screen and (max-width: 500px) {
        .modal-content {
            height: 632px;
        }
    }
</style>