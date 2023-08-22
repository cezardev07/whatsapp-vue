<template>
    <div
        v-bind:class="{verde: verde}"
        class="text-sm bg-white mx-24 my-1 px-3 py-1 rounded-md w-fit"
    >
        {{ conteudo }}
        <span class="text-xs ml-6 text-gray-400">{{ horario }}</span>
    </div>
</template>

<script>
    export default {
        props: ['conteudo', 'horario', 'verde']
    }
</script>

<style>
.verde{
    background: rgb(220, 248, 198) !important;
    align-self: flex-end;
}
</style>