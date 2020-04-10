<template>
    <transition name="modal">
        <div @click="$emit('close')" class="modal-mask">
            <div class="modal-wrapper">
                <div @click="$event.stopPropagation()" class="modal-container">
                    <img :alt="item.Title"
                         :src="item.Poster"
                         onerror="this.src='https://popcornusa.s3.amazonaws.com/placeholder-movieimage.png'">
                    <div class="movieDetails">
                        <h2>{{item.Title}}</h2>
                        <span>{{item.Year}}</span>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name: "MoviePopup",
        props: {
            item: Object
        }
    }
</script>

<style scoped>
    .modal-mask {
        position: fixed;
        z-index: 97;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        display: table;
        transition: opacity 0.3s ease;
    }

    .modal-wrapper {
        z-index: 95;
        display: table-cell;
        vertical-align: middle;
    }

    .modal-container {
        z-index: 99;
        max-width: 80%;
        margin: 0 auto;
        padding: 20px 30px;
        background-color: #fff;
        border-radius: 2px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
        transition: all 0.3s ease;
        font-family: Helvetica, Arial, sans-serif;
    }
</style>