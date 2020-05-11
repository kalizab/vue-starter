<template>
    <div v-if="meetings === null">
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
          meetings: JSON.parse(localStorage.getItem('meetings'))
      };
  },
  methods: {
      addNewMeeting(meeting) {
          if (this.meetings === null){
              this.meetings = []
          }
          this.meetings.push(meeting);
          this.buttonClicked = false;
          localStorage.setItem('meetings', JSON.stringify(this.meetings));
      },
      loadAddNewMeeting() {
      this.buttonClicked = !this.buttonClicked;
    }
  }
}
</script>