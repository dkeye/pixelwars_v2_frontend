<template>
    <form 
        @submit.prevent 
        :id="formID"
        :class="processData.class"
        :key="processData.key"
    >
        <my-input 
            v-model:newPixelSize="processData.information.pixelSize"
        ></my-input>
        <!-- <my-button 
            :eventName="'setPixelSize'"
            :processingData="{
                id: formID,
                class: processData.class,
                key: processData.key,
                information: processData.information,
            }"
        >
            set
        </my-button> -->
    </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'my-form',
    data() {
        return {
            processData: {               
                class: 'my-form',
                key: this.formID + '-' + Date.now(),
                information: {
                    pixelSize: 2,
                },
            }
        }
    },
    
    props: {
        formID: {
            type: String,
            required: true,
        }
    },
    updated() {
        this.$emit('update:setPixelSizeForm', this.processData.information.pixelSize);
    }
})
</script>

<style scoped>

</style>