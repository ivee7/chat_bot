<script>

export default {
    name: 'Message',

    props: {
        outgoing: Boolean,
        text: String,
    },

    computed: {
        classes() {
            return [
                this.outgoing ? 'message__text--outgoing' : 'message__text--incoming'
            ]
        },
    }
}
</script>

<template>
    <div class="message">
        <div class="message__text text-default" :class="classes">
            {{ text }}
        </div>
    </div>
</template>

<style scoped lang="scss">
.message {
    width: fit-content;
    max-width: 80%;

    word-break: break-all;

    &__text {
        padding: 8px;

        border-radius: 10px;

        &--incoming {
            border-bottom-left-radius: 0;
            background-color: #dce3e2;
        }

        &--outgoing {
            border-bottom-right-radius: 0;
            background-color: #b6f2c4;
        }
    }
}
</style>
