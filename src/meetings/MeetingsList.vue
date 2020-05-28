<template>
    <table v-if="meetings.length > 0">
        <thead>
        <tr>
            <th>Nazwa spotkania</th>
            <th>Opis</th>
            <th>Uczestnicy</th>
            <th></th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="meeting in meetings" :key="meeting.name">
            <td>{{ meeting.name }}</td>
            <td>{{ meeting.description }}</td>
            <td><ul><li class="participant-list" v-for="participant in Array.from(meeting.participants)">{{ participant }}</li></ul></td>
            <td>
                <button class="right-button-white" @click="addParticipant(meeting)" v-if="!isParticipantAssigned(meeting)">Zapisz się</button>
                <button class="right-button-white" @click="removeParticipant(meeting)" v-if="isParticipantAssigned(meeting)">Wypisz się</button>
                <button class="right-button" @click="deleteMeeting(meeting)" v-show="meeting.participants.size < 1">Usuń puste spotkanie</button>
            </td>
        </tr>
        </tbody>
    </table>
    <h3 v-else>Brak zaplanowanych spotkań</h3>
</template>

<script>
    export default {
        props: {
            meetings: Array,
            username: String
        },
        methods: {
            deleteMeeting(meeting) {
                const index = this.meetings.indexOf(meeting);
                if (index > -1) {
                    this.meetings.splice(index, 1);
                }
            },
            addParticipant(meeting) {
                this.$emit('updated', meeting.participants.add(this.username));
                this.$forceUpdate();
            },
            isParticipantAssigned(meeting) {
                return meeting.participants.has(this.username);
            },
            removeParticipant(meeting) {
                this.$emit('updated', meeting.participants.delete(this.username));
                this.$forceUpdate();
            }
        }
    }

</script>

<style>
.right-button-white {
    float: right;
    overflow: auto;
    margin: 0px 5px 0px 5px;
    background-color: #FFFFFF;
    color: #9B4DCA;
}
.right-button {
    float: right;
    overflow: auto;
    margin: 0px 5px 0px 5px;
}
.participant-list {
    list-style: circle;
}
</style>
