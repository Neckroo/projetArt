<script setup>
import { ref, computed, watchEffect } from 'vue';
const isClicked = ref(true);

function toggleButton() {
    isClicked.value = !isClicked.value;
    emits('isClicked', isClicked.value);
}

const props = defineProps({
    baseColor: {
        type: String,
        required: false,
        default: "white"
    },
    selectedColor: {
        type: String,
        required: false,
        default: "black"
    },
        baseBorderColor: {
        type: String,
        required: false,
        default: "black"
    },
    selectedBorderColor: {
        type: String,
        required: false,
        default: "white"
    },
    hoverColor: {
        type: String,
        required: false,
        default: "grey"
    },
    value: {
        type: String,
        required: false,
        default: "test"
    }
})

const emits = defineEmits([
    'isClicked'
]);

/*     const value = computed({
    get: () => round(props.modelValue, props.decimalPlaces),
    set: val => {
      if (isNaN(val) || val === '') return;
      emit('update:modelValue', val);
    }
  }); */

</script>

<template>
    <button :class="isClicked ? 'selected' : ''" @click="toggleButton"></button>
</template>



<style scoped>
button {
    width: 20px;
    height: 20px;
    background-color: v-bind('props.baseColor');
    border-radius: 5px;
    border: 1px solid rgb(90, 90, 90);
    cursor: pointer;
    border : 1px solid  v-bind('props.baseBorderColor');
}

button:hover {
    background-color: v-bind('props.hoverColor');
}

button.selected {
    background-color: v-bind('props.selectedColor');
            border : 1px solid  v-bind('props.selectedBorderColor');
}
</style>
