<script setup lang="ts">
import { ref } from 'vue';
const imageSrc = ref<string>('');

const cropsCoords = ref<number[][]>([
    [15, 700], // Первая координата
    [885, 700], // Вторая координата
    [15, 0], // Третья координата
    [885, 0], // Четвертая координата
]);
// Каждый crop имеет координаты, [x, y]
// function showImage(e: FileList) {
    // const imageForm = e.target.files[0];
    // const reader = new FileReader();
    // reader.onload = (t) => {
    // imageSrc.value = t.target.result;
    // };
    // reader.readAsDataURL(imageForm);
// }
// cropNumber = какой именно crop, первый, второй и так далее.
function moveCrop(cropNumber: 1 | 2 | 3 | 4) {
    const coordinateCrop = cropsCoords.value[cropNumber - 1];
    console.log(coordinateCrop);
}

function showCoordinatesAllCrops() {
    console.log(cropsCoords.value);
}
</script>

<template>
    <p class="title">Загрузите ваше изображение</p>
    <input class="input-form" type="file" name="image-src" id="image-src" />
    <div class="viewport-image">
        <div class="image-crop">
            <span @mousedown="moveCrop(1)" class="crop first-crop"></span
            ><span @mousedown="moveCrop(2)" class="crop second-crop"></span
            ><span @mousedown="moveCrop(3)" class="crop three-crop"></span
            ><span @mousedown="moveCrop(4)" class="crop four-crop"></span>
        </div>
        <img class="main-image" alt="" :src="imageSrc" />
    </div>
    <button @click="showCoordinatesAllCrops" class="button-form">
        Сохранить
    </button>
</template>

<style scoped>
img.main-image {
    max-width: 900px;
    max-height: 700px;
    object-fit: cover;
    display: block;
    margin: 0 auto;
    border-radius: 20px;
    filter: contrast(0.5);
}

.viewport-image {
    width: 900px;
    height: 700px;
    border-radius: 20px;
    border: 2px solid rgb(63, 57, 57);
    display: block;
    margin: 0 auto;
    position: relative;
}

.title {
    font-size: 32px;
    font-weight: 300;
    text-align: center;
    width: max-content;
    display: block;
    margin: 0 auto;
}

.input-form {
    display: block;
    margin: 50px auto;
}

button.button-form {
    padding: 10px 30px;
    border-radius: 20px;
    background-color: rgb(41, 169, 41);
    color: white;
    border: none;
    font-size: 24px;
    font-weight: 300;
    display: block;
    text-align: center;
    margin: 26px auto;
}

button.button-form:hover {
    cursor: pointer;
    text-decoration: underline;
}

.image-crop {
    position: absolute;
    width: 100%;
    height: 100%;
    filter: brightness(1);
    z-index: 100;
}

.image-crop span.crop {
    width: 16px;
    height: 16px;
    border: 2px solid black;
    background-color: rgb(75, 65, 65);
    position: absolute;
}

.image-crop span.crop:hover {
    cursor: pointer;
    background-color: rgb(119, 107, 107);
}

.image-crop span.first-crop {
    left: 0%;
    transform: translateX(15px);
}

.image-crop span.second-crop {
    right: 0%;
    transform: translateX(-15px);
}

.image-crop span.three-crop {
    left: 0%;
    bottom: 0%;
    transform: translateX(15px);
}

.image-crop span.four-crop {
    right: 0%;
    bottom: 0%;
    transform: translateX(-15px);
}
</style>
