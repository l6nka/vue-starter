<template>
    <div>
        <h1>System do zapisow na zajęcia</h1>

        <div v-show="authenticatedUsername">
            <user-panel :username="authenticatedUsername" @logout="logMeOut()"></user-panel>
            <meetings-page :username="authenticatedUsername"></meetings-page>
        </div>

        <div v-show="!authenticatedUsername">
            <login-form @login="logMeIn($event)"></login-form>
        </div>

    </div>
</template>

<script>
    import "milligram";
    import LoginForm from "./LoginForm";
    import UserPanel from "./UserPanel";
    import MeetingsPage from "./meetings/MeetingsPage";

    export default {
        components: {LoginForm, MeetingsPage, UserPanel},
        data() {
            return {
                authenticatedUsername: '',
            }
        },
        methods: {
            logMeIn(username) {
                this.authenticatedUsername = username;
            },
            logMeOut() {
                this.authenticatedUsername = '';
            }
        }
    }
</script>
