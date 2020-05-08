<template>
    <div v-if="meetings.length == 0">
        <button @click="loadAddNewMeeting">Dodaj nowe spotkanie</button>
        <div
            v-if="buttonClicked">
            <new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
        </div>
        <label>Brak aktywnych spotkań</label>

    </div>
    <div v-else>
        <h4>Zaplanowane zajęcia ({{meetings.length}})</h4>
        <button @click="loadAddNewMeeting">Dodaj nowe spotkanie</button>
        <div
            v-if="buttonClicked">
            <new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
        </div>
       <meetings-list :meetings="meetings"></meetings-list>
    </div>
</template>

<script>
import NewMeetingForm from "./NewMeetingForm";
import MeetingsList from "./MeetingsList";

export default {
  components: {NewMeetingForm, MeetingsList},
  data() {
      return {
          buttonClicked: false,
          meetings: []
      };
  },
  methods: {
      addNewMeeting(meeting) {
          this.meetings.push(meeting);
          this.buttonClicked = false;
      },
      loadAddNewMeeting() {
      this.buttonClicked = !this.buttonClicked;
    }
  }
}
</script>