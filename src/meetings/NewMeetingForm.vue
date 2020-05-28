<template>
    <form @submit.prevent="addNewMeeting()">
        <h3>Dodaj nowe spotkanie</h3>
        <label>Nazwa</label>
        <input type="text" v-model="newMeeting.name">
        <label>Opis</label>
        <textarea v-model="newMeeting.description"></textarea>
        <button>Dodaj</button><span v-if="isEmptyName" class="warning-msg">Spotkanie musi mieć nazwę!</span>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                newMeeting: {},
                isEmptyName: false
            };
        },
        methods: {
            addNewMeeting() {
                if (this.newMeeting.name) {
                    this.newMeeting.participants = new Set();
                    this.isEmptyName = false;
                    this.$emit('added', this.newMeeting);
                    this.newMeeting = {};
                } else {
                    this.isEmptyName = true;
                }
            }
        }
    }
</script>

<style>
.warning-msg {
    color: red;
    margin-left: 10px;
}
</style>
