<template>
    <div>
        <h3>Zaplanowane zajęcia ({{ meetings.length }})</h3>
        <button v-if="!isAddingMeeting" @click="openNewMeetingForm()">Dodaj spotkanie</button>
        <new-meeting-form v-else @added="addNewMeeting($event)" @updated="updateMeeting($event)"></new-meeting-form>
        <meetings-list :meetings="meetings" :username="username"></meetings-list>
    </div>
</template>

<script>
    import NewMeetingForm from "./NewMeetingForm";
    import MeetingsList from "./MeetingsList";

    export default {
        props: {
            username: String
        },
        components: {NewMeetingForm, MeetingsList},
        data() {
            return {
                meetings: [],
                isAddingMeeting: false
            };
        },
        methods: {
            addNewMeeting(meeting) {
                this.meetings.push(meeting);
                this.isAddingMeeting = !this.isAddingMeeting;
            },
            openNewMeetingForm() {
                this.isAddingMeeting = !this.isAddingMeeting;
            },
            updateMeeting(meeting) {
                this.meetings.forEach( (oldMeeting, index) => {
                        if (oldMeeting.name === meeting.name) {
                            this.meetings[index] = meeting;
                        }
                });
            }
        }
    }
</script>
