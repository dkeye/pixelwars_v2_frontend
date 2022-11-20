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
            type: Number,
            default: 2,        }
    },

    data(){
        return {
            height: function() {
                let inHeight: number = Math.round(window.outerHeight);

                if (inHeight % 10 != 0) {
                    let resultNumb: number = inHeight % 10;
                    inHeight = inHeight - resultNumb;
                };
                return inHeight;
            },
            width: Math.round(window.outerHeight / 2),
            gridColumns: [
                {}
            ],
        }
    },

    mounted() {
        let [canvas, ctx] = this.canvasNewContext();            
        this.generateCanvasGrid(this.pixelSize, canvas, ctx);
        this.canvasСoordinatesXY(canvas);
    },

    methods: {
        canvasNewContext() {
            const canvas:any = this.$refs.myCanvas;
            const ctx = canvas.getContext('2d');
            canvas.height =  window.outerHeight;
            canvas.width = canvas.height / 2 ;
            ctx.strokeStyle = 'rgb(1,222,166)'
            return [canvas, ctx]
        },
        
        generateCanvasGrid(pxSize:number, canvas:any, ctx: any) {
            this.pixGenerate(pxSize);
            let columns = canvas.width / pxSize;
            let rows = Math.round(canvas.height / pxSize);

            window.addEventListener("resize",() => {
                canvas.height = window.outerHeight;
                canvas.width = canvas.height / 2 ;
                pxSize = window.outerHeight / rows;

                if (canvas.width % pxSize != 0) {
                    let result = Math.round(canvas.width % pxSize);
                    canvas.width = canvas.width - result;
                    canvas.height = Math.round(canvas.height - result * 2);
                }

                for (let positionX = 0; positionX < columns ; positionX++) {
                    for(let positionY = 0; positionY < rows ; positionY++) {
                        ctx.strokeRect( pxSize * positionX, pxSize * positionY, pxSize, pxSize);
                    };
                };
            });
        },

        relativeСoordinates(ev:any) {
            return {
                x: ev.pageX - ev.target.offsetLeft,
                y: ev.pageY - ev.target.offsetTop
            };
        },

        canvasСoordinatesXY(canvas:any) {
            canvas.addEventListener('click', (e:any) => {
                const { x, y } = this.relativeСoordinates(e);
                canvas.innerHTML = `X: ${x}, Y: ${y}`;
                console.log('X: ',x,'\nY: ', y)
                console.log(this.getSquarePositionXY(x, y))
            })
            // canvas.addEventListener('mousemove', (e:any) => {
            //     const { x, y } = this.relativeСoordinates(e);
            // });
        },

        pixGenerate(pixSize:any) {
            const canvas:any = this.$refs.myCanvas;
            const ctx = canvas.getContext('2d');
            let gridColumns: any[] = [];
            let gridRow: object[] = [];

            if (this.width % pixSize === 0) {            
                canvas.height = window.outerHeight + (pixSize - (window.outerHeight % pixSize));
                canvas.width = (canvas.height / 2) + ((canvas.height / 2) % pixSize) ;
                let columns = canvas.width / pixSize;
                let rows = canvas.height / pixSize;
                
                for(let positionX = 0; positionX < columns ; positionX++) {
                    for(let positionY = 0; positionY < rows ; positionY++) {
                        ctx.strokeRect( pixSize * positionX, pixSize * positionY, pixSize, pixSize)
                        gridRow.push({
                            positionX,
                            positionY,
                            color: '#000000',
                        });
                    };
                    gridColumns.push(gridRow)
                    gridRow = [];
                };
                this.gridColumns.splice(0, this.gridColumns.length);
                this.gridColumns.push(gridColumns);

            } else {
                let result = this.width % pixSize;
                this.width = this.width - result;
                this.pixGenerate(Number(pixSize));
            }
        },

        getSquarePositionXY(x:number, y:number) {
            return {
                x: Math.floor(x / this.pixelSize),
                y: Math.floor(y / this.pixelSize)
            }
        }
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