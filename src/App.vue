<script>
import Chat from './components/Chat.vue'
import Layout from './components/Layout.vue'

export default {
    name: 'App',

    components: {
        Layout,
        Chat
    }
}
</script>

<template>
    <Layout>
        <Chat />
    </Layout>
</template>

<style scoped>
</style>
