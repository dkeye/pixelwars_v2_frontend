<template>
    <canvas 
        ref='myCanvas'
        id="mainCanvas"
        :key="'myCanvas_' + Date.now()"
    >
        Your browser isn't supported 'canvas' elements.
    </canvas>
</template>

<script lang="ts">
export default {
    name: 'my-field',
    props: {
        pixelSize: {
            type: Number, String,
        }
    },
    data(){
        return {
            height: Math.round(window.innerHeight * 0.9),
            width: Math.round((window.innerHeight * 0.9) / 2),
        }
    },

    mounted() {
        let [canvas, ctx] = this.canvasNewContext();            
        this.generateCanvasGrid(this.pixelSize, canvas, ctx);
        this.canvasCoorsXY(canvas);
    },

    updated() {
        let [canvas, ctx] = this.canvasNewContext();            
        this.generateCanvasGrid(this.pixelSize, canvas, ctx);
    },

    methods: {
        canvasNewContext() {
            const canvas:any = this.$refs.myCanvas;
            const ctx = canvas.getContext('2d');
            canvas.height =  window.innerHeight * 0.9;
            canvas.width = canvas.height / 2 ;
            ctx.strokeStyle = 'rgb(1,222,166)'
            return [canvas, ctx]
        },
        
        generateCanvasGrid(pxSize:any, canvas:any, ctx: any) {
            console.log(pxSize)
            this.pixGenerate(pxSize);

            window.onresize= function(){
                canvas.height =  window.innerHeight * 0.9;
                canvas.width = canvas.height / 2 ;
                let widthPix = Math.floor(canvas.width / pxSize);
                let heightPix = canvas.height / pxSize;

                if (canvas.width % pxSize != 0) {
                    let result = canvas.width % pxSize;
                    canvas.width = canvas.width - result;
                    canvas.height = canvas.height + Math.floor(result / 2);
                    ctx.strokeStyle = 'rgb(1,222,166)'
                }

                for (let numHrzPixel = 1; numHrzPixel < widthPix - 1 ; numHrzPixel++) {
                    for(let numVrtPixel = 1; numVrtPixel < heightPix - 1 ; numVrtPixel++) {
                        ctx.strokeRect( pxSize * numHrzPixel, pxSize * numVrtPixel, pxSize, pxSize)
                    };
                };
            };
        },

        relativeCoors(ev:any) {
            return {
                x: ev.pageX - ev.target.offsetLeft,
                y: ev.pageY - ev.target.offsetTop
            };
        },

        canvasCoorsXY(canvas:any) {
            canvas.addEventListener('mousemove', (e:any) => {
                const { x, y } = this.relativeCoors(e);
                canvas.innerHTML = `X: ${x}, Y: ${y}`;
                console.log('X: ',x,'\nY: ', y)
            });
        },

        pixGenerate(pixSize:any) {
            if (this.width % pixSize === 0) {
                const canvas:any = this.$refs.myCanvas;
                const ctx = canvas.getContext('2d');
                let widthPix = Math.floor(this.width / pixSize);
                let heightPix = this.height / pixSize;

                for(let numHrzPixel = 1; numHrzPixel < widthPix - 1 ; numHrzPixel++) {
                    for(let numVrtPixel = 1; numVrtPixel < heightPix - 1 ; numVrtPixel++) {
                        ctx.strokeRect( pixSize * numHrzPixel, pixSize * numVrtPixel, pixSize, pixSize)
                    };
                };
            } else {
                let result = this.width % pixSize;
                this.width = this.width - result;
                this.height = this.height + Math.floor(result / 2);
    
                if (pixSize == "") {
                    this.$emit('update:setPixelSizeField', 0);
                } else {
                    this.pixGenerate(Number(pixSize));
                }
            }
        },
    }
};
</script>

<style scoped>
  #mainCanvas {
        border: 2px solid black;
        background: #FFFFFF;
        margin: 3px;
    }
</style>