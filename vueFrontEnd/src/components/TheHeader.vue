<script setup>
import { ref, computed, watchEffect } from 'vue';
import TheBurger from './TheBurger.vue';
import TheProfile from './TheProfile.vue';
import TheSelection from './TheSelection.vue';
import { user} from "../state.js";
import { useFetch } from '../composables/fetch.js';
import { apiHoraireBase } from "../config/horaires.js"
import { myClass, urlFinale } from "../state.js";

const { data: allCourses } = useFetch("https://abe-pingouin.heig-vd.ch/horairetoutesclasses");

const tabClasses = computed(() => {
    if (allCourses.value?.length > 0) {
        return Array.from(new Set(allCourses.value.map(d => d.classe)));
    } else {
        return [];
    }
});

</script>

<template>
    <div class="container_header">
        <the-burger></the-burger>
                <the-selection v-if="user=='teacher' || user=='anonymous'" @changeClasse="myClass = $event" v-bind:classes=tabClasses></the-selection>
        <the-profile></the-profile>
    </div>
</template>



<style scoped>
.container_header {
    width: 100%;
    min-height: 70px;
    
    top: 0;
    display: flex;
    flex-direction: row;
    flex-basis: auto;
    justify-content: space-between;
    background-color: #262626;
    border-bottom: 1px solid #E7F0FF

}
</style>
