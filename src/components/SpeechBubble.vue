<template>

<div class="speech-bubble" :key="text">
    <p >{{text}}</p>
</div>
</template>

<script>
export default {
    name: 'SpeechBuuble',
    props: ["text"],
    data: function() {
        return {}
    },
    methods: {}
}
</script>

<style scoped>
.speech-bubble {
	position: relative;
    background: white;
    max-width: 400px;
    border: 2px solid black;
    border-radius: .4em;
    padding: 18px;
}

.speech-bubble:before {
	content: '';
	position: absolute;
	bottom: 0;
	left: 7%;
	width: 0;
	height: 0;
	border: 20px solid transparent;
	border-top-color: black;
	border-bottom: 0;
	border-left: 0;
	margin-left: -10px;
	margin-bottom: -20px;
}
.speech-bubble:after {
	content: '';
	position: absolute;
	bottom: 0;
	left: 7%;
	width: 0;
	height: 0;
	border: 15px solid transparent;
	border-top-color: white;
	border-bottom: 0;
	border-left: 0;
	margin-left: -8px;
	margin-bottom: -15px;
}
</style>