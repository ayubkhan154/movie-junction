<template>
    <div :style="`background: url('${poster}')`" @click="$emit('click')" class="poster">
        <img :alt="title" :src="poster">
        <div class="posterOverlay">
            {{title}}<br><br>({{year}})
        </div>
    </div>
</template>

<script>
    export default {
        name: "MoviePortrait",
        props: {
            poster: String,
            title: String,
            year: String
        }
    }
</script>

<style scoped>
    .poster {
        margin: 0;
        border-radius: 4px;
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.23);
        transition: all 0.3s;
        overflow: hidden;
    }

    .poster img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        object-position: center center;
        backdrop-filter: blur(4px) brightness(0.5);
    }

    .posterOverlay {
        margin: 0;
        font-size: medium;
        position: absolute;
        width: 100%;
        height: 100%;
        text-align: center;
        color: whitesmoke;
        display: none;
        transition: all 0.3s;
    }

    .poster:hover {
        cursor: pointer;
        transform: translateY(-4px);
        box-shadow: 0 3px 9px 0 rgba(0, 0, 0, 0.65);
    }

    .poster:hover .posterOverlay {
        top: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        backdrop-filter: brightness(0.3) blur(4px);
        word-break: break-word;
    }
</style>