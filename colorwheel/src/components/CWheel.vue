<template>
    <div id="container">
        <color-picker :key="componentKey" v-model.number="color.hue" v-bind="{msg, color}" variant="persistent" @input="onInput" @select="onColorSelect"/>
        <h1 v-text="color.hue.toFixed(1)"></h1> <h2 v-text="msg.msg"></h2>
        <div id="response">
        <button @click="()=>msg.msg='sent'">Submit</button>
        <button @click="()=>{
            msg.msg='';
            color.hue=0;
            forcReload();
            }">Reset</button>
        </div>
    </div>
</template>

<script lang="ts">
    import { reactive } from 'vue';
    import ColorPicker from '@radial-color-picker/vue-color-picker';
    let msg: string;
    let hueVal: number;

    export default {
        components: { ColorPicker },
        setup() {
            const msg = reactive({
                msg: "",
            });

            const color = reactive({
                hue: 0,
                saturation: 100,
                luminosity: 50,
                alpha: 1,
            });


            return {
                color,
                msg,
                hueVal,
                componentKey: 0,
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
                onChange(hue:number)
                {
                    console.log("Hue changed to: " + hue);
                    color.hue = hue;
                }
            };
        },
        methods: {
            forcReload() {
                this.componentKey += 1;
            },
        }
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

    #container {
        display: flex;
        flex-direction: column;
        justify-content: center;
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
        justify-content: center;
        align-content: center;
        align-self: center;
        align-items: center;
        width: 100%;
    }
</style>