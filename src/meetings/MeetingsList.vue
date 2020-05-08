<template>
    <table v-if="meetings.length > 0">
        <thead>
            <tr>
                <th>Nazwa spotkania</th>
                <th>Opis</th>
                <th>Uczestnicy</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="meeting in meetings" :key="meeting.name">
                <td>{{ meeting.name }}</td>
                <td>{{ meeting.description }}</td>
                <td v-if="meetingAttendents.length !=0">{{meetingAttendents}}</td>
                <td v-else> - </td>
                <br>
                <br>
                <button @click="saveToMeeting(authenticatedUsername)"> Zapisz się</button>
                <button @click="deleteMeeting(meeting.newMeetingID)">Usuń spotkanie</button>
            </tr>
        </tbody>
    </table>
</template>

<script>

export default {
  props: ['meetings', 'authenticatedUsername'],
  data() {
      return {
          meetingAttendents: []
        //   meetings: []
      };
  },
  methods: {
      saveToMeeting(user) {
          this.meetingAttendents.push(user)
        },

      deleteMeeting(meeting) {
          this.meetings.pop(meeting)
        },
  }
}



// export default {
//     props: ['meetings'],

//     methods: {
//         deleteMeeting(meeting) {
//             this.meetings.pop(meeting)
//         },
//         deleteMeeting(meeting) {
//             this.meetings.pop(meeting)
//         }
//     }
// }
</script>