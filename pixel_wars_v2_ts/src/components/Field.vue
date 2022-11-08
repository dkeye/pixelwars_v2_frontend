<template>
    <canvas ref='myCanvas' id="mainCanvas">
    </canvas>
</template>

<script lang="ts">
 
export default {

        mounted() {
            const canvas:any = this.$refs.myCanvas
            const ctx = canvas.getContext('2d') 

            for (let i:number = 0; i < 50; i++) {
                for (let j:number = 0; j < 50; j++) {
                    ctx.fillStyle = `rgb(
                        ${Math.floor(255 - 16 * i)},
                        ${Math.floor(255 - 16 * j)},
                        100)`;
                    ctx.fillRect(j * 10, i * 10, 10, 10);
                }
            } 
        },
    };
</script>

<style scoped>
    #mainCanvas {
        width: 500px;
        height: 500px;
        border: 2px solid black;
        background: #FFFFFF;
    }
</style>