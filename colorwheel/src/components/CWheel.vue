<template>
    <div id="container">
        <color-picker v-bind="color" variant="persistent" @input="onInput" @select="onColorSelect"/>
        <h1 v-text="color.hue.toFixed(3)"></h1>
        <div id="response">
        <button>Submit</button>
        <button>Random</button>
        </div>
    </div>
</template>

<script lang="ts">
    import { reactive } from 'vue';
    import ColorPicker from '@radial-color-picker/vue-color-picker';

    export default {
        components: { ColorPicker },
        setup() {
            const color = reactive({
                hue: 50,
                saturation: 100,
                luminosity: 50,
                alpha: 1,
            });

            return {
                color,
                onInput(hue: number) {
                    console.log("Hue changed to: " + hue);
                    color.hue = hue;
                },
                onColorSelect(color: {
                    hue: number;
                    saturation: number;
                    luminosity: number;
                    alpha: number;
                }) {
                    console.log("Color selected: ");
                    console.log(color);
                },
            };
        },
    };
</script>

<style>
    @import '@radial-color-picker/vue-color-picker/dist/vue-color-picker.min.css';

    h1 {
        display: flex;
        flex-direction: column;
        width: 20rem;
        margin: auto;
        margin-top: 5vh;
        align-content: center;
        align-self: center;
        align-items: center;
    }

    #response {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        margin-top: 5vh;
        width: auto;
    }

    #response > button {
        width: 5rem;
        height: 3rem;
        font-size: 1rem;
        margin: 4px;
    }

    #container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-content: center;
        align-self: center;
        align-items: center;
    }
</style>