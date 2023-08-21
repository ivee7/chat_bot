<script>
export default {
    name: 'SendSVG',

    props: {
        class: String
    },

    computed: {
        classes() {
            return {
                [this.class]: !!this.class
            }
        }
    }
}
</script>

<template>
    <svg class="send-svg" :class="classes" xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960" fill="currentColor">
        <path d="M120-160v-640l760 320-760 320Zm60-93 544-227-544-230v168l242 62-242 60v167Zm0 0v-457 457Z"/>
    </svg>
</template>

<style scoped>
.send-svg {
    height: 48px;
    width: 48px;
}
</style>