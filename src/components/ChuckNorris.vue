<template>
<div id="chuck-norris">
    <img src="../assets/chuck norris.jpg" id="chuck-norris__image" @click="fetchRandomJoke()">
    <transition name="fade" mode="out-in">
        <speech-bubble id="chuck-norris__joke__container" :text="currentJoke.joke" v-if="currentJoke" />
    </transition>
</div>
</template>

<script>
import SpeechBubble from './SpeechBubble.vue'

import axios from 'axios'

const API_RANDOM_JOKE_ENDPOINT = 'http://api.icndb.com/jokes/random'

export default {
    name: 'ChuckNorris',
    components: {
        SpeechBubble
    },
    mounted() {
        this.fetchRandomJoke()
    },
    data: function() {
        return {
            currentJoke: null
        }
    },
    methods: {
        fetchRandomJoke() {
            axios.get(API_RANDOM_JOKE_ENDPOINT)
                .then(({ data }) => {
                    this.currentJoke = data.value
                    this.currentJoke.joke = this.currentJoke.joke.replace(/&quot;/g, '"')
                })
        }
    }
}
</script>

<style scoped>
#chuck-norris {
    position: relative;
    margin-top: 400px;
    width: 500px;
}

#chuck-norris__image {
    width: 100%;
    /* height: 200px; */
    transition: all 0.2s ease-in;
}

#chuck-norris__image:hover {
    transform: scale(1.1);
}

#chuck-norris__joke__container {
    position: absolute;
    bottom: calc(100%);
    left: 25%;
    z-index: 99;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s
}

.fade-enter,
.fade-leave-to
/* .fade-leave-active below version 2.1.8 */

{
    opacity: 0
}
</style>
