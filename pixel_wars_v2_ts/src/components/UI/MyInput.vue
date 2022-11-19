<template>
    <input 
        :value="inputValue" 
        @input="updateInput" 
        class="my-input" 
        type="number" 
        placeholder="Size of pixels"
        min="2" 
        max="20"
    >
</template>

<script lang="ts">
import { toNumber } from '@vue/shared';

export default {
    name: 'my-input',

    data() {
        return {
            inputValue: '',
        }
    },
    
    methods: {
        updateInput(event: any) {
            this.inputValue = toNumber(event.target.value);
            console.log(this.inputValue)
            this.$emit('update:newPixelSize', this.inputValue)
        }
    }
}
</script>

<style scoped>
    .my-input {
        width: 6rem;
    }
</style>