<script>
export default {
    name: 'Layout',
}
</script>

<template>
    <div class="layout">
        <slot />
    </div>
</template>

<style scoped lang="scss">
.layout {
    width: 100%;
    height: 100%;
    padding: 10px;

    background: linear-gradient(0deg, rgba(0,82,32,1) 0%, rgba(66,255,54,1) 100%);;

    @media (min-width: $media-mobile) {
        display: flex;
        align-items: center;
        justify-content: center;
    }
}
</style>
