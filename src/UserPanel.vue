<template>
    <div>
        <h2>Witaj {{ username }}!</h2>
        <button class="logout-button" @click="$emit('logout')">Wyloguj</button>
    </div>
</template>

<script>
    export default {
        props: ['username']
    }
</script>

<style>
.logout-button {
    float: right;
    overflow: auto;
    background-color: #FFFFFF;
    color: #9B4DCA;
}
</style>
