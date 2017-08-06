<template>
<div id="chuck-norris" :style="{'height':height ? height : '100%'}">
    <img src="../assets/chuck norris.jpeg" id="chuck-norris__image" @click="fetchRandomJoke()"  :style="{'height':height ? height : 'auto'}">
    <transition name="fade" mode="out-in">
        <speech-bubble id="chuck-norris__joke__container" :text="currentJoke.joke" :style="{'left': offset}" v-if="currentJoke" />
    </transition>
</div>
</template>

<script>
import SpeechBubble from './SpeechBubble.vue'

import axios from 'axios'

const API_RANDOM_JOKE_ENDPOINT = 'https://api.icndb.com/jokes/random'

export default {
    name: 'ChuckNorris',
    props: ["height"],
    components: {
        SpeechBubble
    },
    mounted() {
        this.fetchRandomJoke()

        document.querySelector('img').addEventListener('load',() => {
            this.getBubbleOffset()
        })

        window.addEventListener('resize', (e) => this.getBubbleOffset())
    },
   
    beforeDestroy() {
        window.addEventListener('resize', (e) => this.getBubbleOffset())
    },
    data: function() {
        return {
            currentJoke: null,
            offset: null
        }
    },
    methods: {
        getBubbleOffset() {
            this.offset = ((document.getElementById('chuck-norris__image').clientWidth) * (1 / 3)) + "px"
        },
        fetchRandomJoke() {
            axios.get(API_RANDOM_JOKE_ENDPOINT)
                .then(({
                    data
                }) => {
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
}

#chuck-norris__image {
    max-width: 100%;
    width: auto;
    height: auto;
    transition: all 0.2s ease-in;
}

#chuck-norris__image:hover {
    transform: scale(1.1);
}

#chuck-norris__joke__container {
    position: absolute;
    bottom: calc(100%);
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
