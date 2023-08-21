<script>
import Message from './Message.vue';
import Suggestion from './Suggestion.vue';
import RobotSVG from '../assets/icons/RobotSVG.vue';
import PersonSVG from '../assets/icons/PersonSVG.vue';

export default {
    name: 'Messages',

    props: {
        messages: Array,
    },

    components: {
        Message,
        Suggestion,
        RobotSVG,
        PersonSVG
    },

    methods: {
        showAuthor(item, index) {
            return this.messages[index + 1]?.outgoing !== item.outgoing;
        },

        blockClasses(item, index) {
            const classes = [];

            if (!this.showAuthor(item, index)) classes.push('messages__block--pushed');
            if (item.outgoing) classes.push('messages__block--reverse');

            return classes;
        },

        authorClasses(outgoing) {
            return outgoing ? 'messages__author-icon--beige' : 'messages__author-icon--blue'
        },

        authorComonent(outgoing) {
            return outgoing ? 'PersonSVG' : 'RobotSVG';
        },

        onSuggestionClick(suggestion) {
            this.$emit('suggestion:click', suggestion);
        },
    }
}
</script>

<template>
    <ul class="messages">
        <li
            v-for="(message, index) in messages"
            :key="index"
            class="messages__item"
        >
            <div
                class="messages__block"
                :class="blockClasses(message, index)"
            >
                <div
                    v-if="showAuthor(message, index)"
                    class="messages__author"
                >
                    <component
                        :is="authorComonent(message.outgoing)"
                        class="messages__author-icon"
                        :class="authorClasses(message.outgoing)"
                    />
                </div>

                <Message
                    :outgoing="message.outgoing"
                    :text="message.text"
                />
            </div>

            <div v-if="message.suggestions" class="messages__block messages__block--sub">
                <Suggestion
                    v-for="suggestion in message.suggestions"
                    :outgoing="message.outgoing"
                    :suggestion="suggestion"
                    @click="onSuggestionClick(suggestion)"
                    class="messages__suggestion"
                />
            </div>
        </li>
    </ul>
</template>

<style scoped lang="scss">
.messages {
    $icon-size: 28px;
    $icon-margin: 6px;
    $block-margin: calc($icon-size + $icon-margin);

    display: flex;
    flex-direction: column;

    width: 100%;

    &__item {
        margin-bottom: 10px;
    }

    &__author {
        display: flex;

        width: $icon-size;
        height: $icon-size;
        padding: 2px;
        margin-right: $icon-margin;

        border-radius: 50%;
        box-shadow: 0px 1px 2px #000000;

        :deep(.messages__author-icon) {
            width: $icon-size;
            height: $icon-size;
        }

        :deep(.messages__author-icon--blue) {
            color: #1300a3;
        }

        :deep(.messages__author-icon--beige) {
            color: #e0b46c;
        }
    }

    &__block {
        display: flex;

        &--sub {
            flex-wrap: wrap;

            margin-top: 10px;
            margin-left: $block-margin;
        }

        &--reverse {
            flex-direction: row-reverse;
        }

        &--pushed {
            margin-left: $block-margin;
        }

        &--reverse.messages__block--pushed {
            margin-left: 0;
            margin-right: $block-margin;
        }

        &--reverse .messages__author {
            margin-right: 0;
            margin-left: $icon-margin;
        }
    }

    &__suggestion {
        margin-right: 10px;

        @include zero-horizontal-offset-of-last;
    }
}
</style>
