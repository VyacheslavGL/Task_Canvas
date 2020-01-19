<template>
    <v-container>
        <v-layout column>
            <h1>Rotation of the triangle on the Y axis</h1>
            <v-row
                    class="ma-auto"
            >
                <v-col
                        cols="12"
                        md="12"
                >
                    <canvas id="canvas" ref="canvas" width="1000" height="400">
                        <p>Ваш браузер не поддерживает Canvas</p>
                    </canvas>
                </v-col>
            </v-row>

        </v-layout>
        <v-layout>
            <v-row
                    justify="center"
                    class="mx-auto"
            >
                <v-col
                        cols="5"
                        md="5"
                >
                    <h2>Выбор направления вращения фигуры</h2>

                    <v-switch
                            class="d-md-inline-block"
                            v-model="switch1"
                            :label="`Поворот: ${ChangeRotate}`"
                    ></v-switch>

                </v-col>
                <v-col
                        cols="5"
                        md="5"
                >
                    <h2>Выбор цвета фигуры</h2>

                    <v-color-picker
                            class="ma-2"
                            hide-canvas
                            v-model="color"
                            mode="hexa"
                    ></v-color-picker>
                </v-col>
            </v-row>
        </v-layout>
    </v-container>
</template>

<script>
    export default {
        name: "Canvas",
        data() {
            return {
                color: '',
                switch1: false,
                canvas: null,
                context: null,
            }
        },
        methods: {
            draw() {

                this.canvas = document.getElementById('canvas');
                // this.canvas = this.$refs.clear;
                // this.canvas.width = window.innerWidth;
                // this.canvas.height = window.innerHeight;
                this.context = this.canvas.getContext("2d");

                //changing the context
                let myThis = this;

                setInterval(() => {

                    // Moves the canvas and its origin on the grid. x indicates the horizontal distance to move,
                    // and y indicates how far to move the grid vertically.
                    myThis.context.translate(myThis.canvas.width, 0);

                    // Scales the canvas units by x horizontally and by y vertically. Both parameters are real numbers.
                    // Values that are smaller than 1.0 reduce the unit size and values above 1.0 increase the unit size.
                    // Values of 1.0 leave the units the same size.
                    myThis.context.scale(-1, 1);

                    // Erases the pixels in a rectangular area by setting them to transparent black.
                    myThis.context.clearRect(0, 0, myThis.canvas.width, myThis.canvas.height);

                    // color rectangle
                    myThis.context.fillStyle = this.color;
                    // draw a rectangle
                    myThis.context.fillRect(30, 30, 50, 50);

                    //draw a triangle
                    myThis.context.beginPath();
                    myThis.context.moveTo(myThis.canvas.width / 2 - 20, myThis.canvas.height / 2);
                    myThis.context.lineTo(myThis.canvas.width / 2 - 100, myThis.canvas.height / 2 + 100);
                    myThis.context.lineTo(myThis.canvas.width / 2 + 100, myThis.canvas.height / 2 + 100);
                    myThis.context.fill();

                    //draw a circle inside the triangle
                    myThis.context.fillStyle = '#b52700';
                    myThis.context.beginPath();
                    myThis.context.arc(myThis.canvas.width / 2 - 70, myThis.canvas.height / 2 + 85, 5, 0, Math.PI * 2, true);
                    myThis.context.fill();
                    myThis.context.stroke();
                }, 1000);
            },
        },
        computed: {
            ChangeRotate() {
                return this.switch1 ? 'по часовой' : 'против часовой';
            }
        },
        mounted() {
            this.draw();
        },
    }
</script>

<style scoped>
    canvas {
        margin-top: 50px;
        border: 1px solid red;
    }
</style>