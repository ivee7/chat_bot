<script>
export default {
    name: 'Suggestion',

    props: {
        suggestion: Object,
        outgoing: Boolean
    }
}
</script>

<template>
    <button v-bind="$attrs" class="suggestion text-default">
        {{ suggestion.text }}
    </button>
</template>

<style scoped lang="scss">
.suggestion {
    padding: 8px;

    border: 1px solid #4a9377;
    border-radius: 10px;
    background-color: #dce3e2;

    &:hover {
        background-color: #4a9377;
    }
}
</style>
