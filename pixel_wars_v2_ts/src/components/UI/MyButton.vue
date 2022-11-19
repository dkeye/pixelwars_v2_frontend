<template>
    <button class='my-button' @click="clickEvent" > 
        <slot></slot>
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'my-button',
    props: {
        eventName: {
            type: String,
            required: true,
        },
        processingData: {
            type: Object,
            required: true,
            default: {
                id: '',
                class: '',
                key: '',
                information: {},
            }
        } 
    },
    setup () {
        return {
        }
    },
    methods: {
        clickEvent() {
            console.log(this.processingData)
            console.log(this.eventName)
            this.$emit('update:' + this.eventName, this.processingData)
        }
    }
})
</script>

<style scoped>
    .my-button {
        text-align: center;
        white-space: nowrap;
        vertical-align: middle;
        color: #fff;
        border: 0.1rem solid transparent;
        background-color:#28a745;
        user-select: none;
        border-radius: 0.25rem;
        padding: 0.05rem 0.6rem;
        font-size: 1rem;
        line-height: 1;
        transition: color .05s ease-in-out,background-color .05s ease-in-out,border-color .05s ease-in-out,box-shadow .05s ease-in-out;
    }
    .my-button:hover {
        background-color:rgb(228, 228, 228);
        cursor: pointer;
        color: #fff;
        background-color: #218838;
        border-color: #1e7e34;
    }
</style>