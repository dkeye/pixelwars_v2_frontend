<template>
    <div 
        :style="rgbBackground">
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Pixel',
        data () {
            return {

            };
        },
        props: {
            rgbBackground: {
                type: Object,
            }
        }
    }
</script>

<style scoped>
    div {
        width: 4px;
        height: 4px;
    }
</style>