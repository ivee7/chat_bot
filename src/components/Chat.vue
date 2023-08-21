<script>
import Messages from './Messages.vue';
import SendSVG from '../assets/icons/SendSVG.vue';

export default {
    name: 'Chat',

    components: {
        Messages,
        SendSVG
    },

    data() {
        return {
            inputText: '',
            messages: []
        }
    },

    mounted() {
        if (!this.messages.length) {
            this.pushMessage(false, 'Привет! Что я могу для Вас сделать?', [
                {
                    text: 'Заказать пиццу',
                    reply: 'Хорошо, я закажу пиццу. Что еще могу сделать?'
                },
                {
                    text: 'Установить будильник',
                    reply: 'Хорошо, я установлю будильник. Что-то ещё потребуется?'
                },
                {
                    text: 'Вывести погоду',
                    reply: 'Вывожу погоду на сегодня'
                }
            ])
        }
    },

    methods: {
        pushMessage(outgoing, text, suggestions) {
            this.messages.push({outgoing, text, suggestions})
        },

        onSuggestionClick(suggestion) {
            this.pushMessage(true, suggestion.text);
            this.pushMessage(false, suggestion.reply);
        },

        onSendButtonClick() {
            if (this.inputText.trim()) {
                this.pushMessage(true, this.inputText);
                this.inputText = '';
            }
        }
    }
}
</script>

<template>
    <div class="chat">
        <div class="chat__space">
            <Messages
                :messages="messages"
                @suggestion:click="onSuggestionClick"
            />
        </div>

        <form class="chat__bar">
            <input
                class="chat__input text-default"
                placeholder="Введите текст..."
                v-model="inputText"
            />

            <button
                class="chat__send-btn"
                @click.prevent="onSendButtonClick"
            >
                <SendSVG class="chat__send-btn-icon"/>
            </button>
        </form>
    </div>
</template>

<style lang="scss" scoped>
.chat {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    width: 100%;
    height: 100%;
    padding: 10px 10px;

    border-radius: 20px;
    background-color: #ffffff;

    @media (min-width: $media-mobile) {
        max-width: 600px;
        padding: 14px 14px;
    }

    @media (min-width: $media-laptop) {
        max-width: 800px;
        padding: 16px 16px;
    }

    &__bar {
        display: flex;
        align-items: center;

        width: 100%;
        padding-top: 4px;
        padding-bottom: 4px;

        border-top: 2px solid #8acfc4;
    }

    &__input {
        flex-grow: 1;

        height: 100%;
        padding-left: 4px;
        padding-right: 4px;

        border-right: 2px solid #8acfc4;

        &::placeholder {
            font-size: 1.2rem;

            color: #8acfc4;

            @media (min-width: $media-mobile) {
                font-size: 1.4rem;
            }

            @media (min-width: $media-laptop) {
                font-size: 1.8rem;
            }
        }
    }

    &__send-btn {
        display: flex;

        padding-left: 4px;

        &:active {
            transform: scale(0.96);
        }

        &:hover & {
            &-icon {
                color: #2fae45;
            }
        }

        &-icon {
            color: #8acfc4;
        }
    }

    &__space {
        display: flex;
        overflow-y: auto;
        flex-direction: column-reverse;

        padding-right: 6px;
        margin-bottom: 4px;

        &::-webkit-scrollbar {
            width: 4px;
        }

        &::-webkit-scrollbar-thumb {
            background-color: rgba(43, 150, 72, 0.3);
            border-radius: 2px;
        }

        &::-webkit-scrollbar-track {
            background-color: transparent;
        }
    }
}
</style>
