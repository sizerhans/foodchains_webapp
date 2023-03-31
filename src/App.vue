
<script>
import Buttons from './../app/Buttons.vue'
import plantData from './json/plants.json'
import animalData from './json/animals.json'
export default {
    components: {
        Buttons
    },
    data() {
        return {
            plantData: plantData,
            animalData: animalData,
            labels: []
        }
    },
    methods: {
    },
};
//the html for the page
</script>
<template>
    <!--html for the camera defined in index.js-->
    <div class="camera">
        <video id="video">Video stream not available.</video>
        <button id="startbutton">Take photo</button>
    </div>
    <canvas id="canvas"> </canvas>
    <div class="output">
        <img id="photo" alt="The screen capture will appear in this box." />
    </div>
    <h2>Describe your Photo</h2>
    <!--dynamic Button component passes Json files-->
    <Buttons 
    v-bind:plantJson="plantData"
    v-bind:animalJson="animalData"
     />
</template>