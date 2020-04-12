<template>
    <transition name="modal">
        <div @click="$emit('close')" class="modal-mask">
            <div class="modal-wrapper">
                <div :style="`background-image: url('${item.Poster}')`" @click="$event.stopPropagation()"
                     class="modal-container">
                    <div class="image">
                        <img :alt="item.Title"
                             :src="item.Poster"
                             onerror="this.src='https://popcornusa.s3.amazonaws.com/placeholder-movieimage.png'">
                    </div>
                    <div class="movieDetails">
                        <h2>{{item.Title}}</h2>
                        <p class="time">
                            <font-awesome-icon :icon="['fad', 'calendar']"/>
                            {{item.Year}}&nbsp;
                            <font-awesome-icon :icon="['fad', 'clock']"/>
                            {{item.Runtime}}
                        </p>
                        <p class="votes">
                            <font-awesome-icon :icon="['fab', 'imdb']"/>
                            {{item.imdbRating}}/10 in {{item.imdbVotes}} votes
                        </p>
                        <br>
                        <p class="genre"><span class="itemHead">Genre: </span>{{item.Genre}}</p>
                        <p class="cast"><span class="itemHead">Cast: </span>{{item.Actors}}</p>
                        <p class="plot">{{item.Plot}}</p>
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
        background-color: rgba(0, 0, 0, 0.8);
        color: #FFF;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: opacity 0.3s ease;
        backdrop-filter: brightness(0.5);
    }

    .modal-wrapper {
        z-index: 98;
        display: table-cell;
        vertical-align: middle;
    }

    .modal-container {
        background-repeat: no-repeat;
        background-size: cover;
        background-position: top center;
        display: grid;
        grid-template-columns: auto 1fr;
        z-index: 99;
        overflow: hidden;
        margin: 0 auto;
        background-color: #000;
        border-radius: 5px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33), inset 0 0 100px 25px #000;
        transition: all 0.3s ease;
        font-family: 'Segoe UI', Helvetica, Arial, sans-serif;
    }

    .image {
        margin: 0;
        padding: 0;
        display: flex;
    }

    .image img {
        margin: 0;
        padding: 0;
        object-fit: cover;
    }

    .movieDetails {
        backdrop-filter: blur(15px) brightness(0.2);
        text-align: start;
        padding: 0 1em;
        margin: 0;
        border: 0;
    }

    .movieDetails h2 {
        font-family: 'IBM Plex Serif', serif;
        font-weight: 400;
        margin: 0.25em 0 0.5em;
        font-size: 2em;
        text-shadow: 0 0 5px #FFFFFFA0;
    }

    .movieDetails p {
        margin: 0 0 0.5em;
        font-size: 0.8em;
        font-family: 'IBM Plex Sans', sans-serif;
    }

    .movieDetails p.plot {
        font-family: 'IBM Plex Sans', sans-serif;
        font-size: 1em;
        margin: 0.8em 0;
        max-width: 65ch;
        line-height: 1.6;
        /*font-style: italic;*/
    }

    .itemHead {
        font-style: italic;
        font-weight: bold;
    }
</style>