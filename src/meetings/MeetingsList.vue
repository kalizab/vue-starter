<template>
    <table :key="componentKey" v-if="meetings.length > 0">
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
                <td v-if="getAttendeeQuantity(meeting.attendees) > 0">
                    <label v-for="attendee in meeting.attendees" :key="attendee">{{attendee}}</label>
                </td>
                <td v-else-if="getAttendeeQuantity(meeting.attendees) == 0">
                    <label>-</label>
                </td>
                <td v-else>
                    <label>-</label>
                </td>
                <td v-if="isAttendeeExist(meeting.attendees, userAttendee) === false">
                    <button v-if="meeting.attendees != userAttendee" @click="saveToMeeting(meetings, meeting.name, userAttendee)">Zapisz się</button>
                </td>
                <td v-if="isAttendeeExist(meeting.attendees, userAttendee) === true">
                    <button @click="removeFromMeeting(meetings, meeting.attendees, meeting.name, userAttendee)">Wypisz się się</button>
                </td>
                <td>
                    <button v-if="getAttendeeQuantity(meeting.attendees) == 0" @click="deleteMeeting(meetings, meeting.name)">Usuń puste spotkanie</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
  props: ['meetings'],
  data() {
      return {
          componentKey: 0,
          userAttendee: JSON.parse(localStorage.getItem('loginUser'))
      };
  },
  methods: {
      saveToMeeting(meetings, meeting, user) {
          for (var i = 0; i < meetings.length; i++) {
              if(meeting === meetings[i].name){
                  if (meetings[i].attendees == null){
                      meetings[i].attendees = [user];
                  }
                  else if (meetings[i].attendees != user){
                      meetings[i].attendees.push(user)
                  }
              }
            }
              localStorage.setItem("meetings", JSON.stringify(meetings));
              this.componentKey += 1;
        },

    isAttendeeExist(attendees, user){
        if (attendees == null){
            return false;
        }
        else{
            for(var i=0; i < attendees.length; i++){
                if( attendees[i] == user){
                    return true
                    }
                }
            return false
        }
    },

        getAttendeeQuantity(attendees){
        if (attendees == null){
            return 0;
        }
        else{
            return attendees.length
        }
    },

       removeFromMeeting(meetings, attendees, meeting, user) {
          for (var i = 0; i < meetings.length; i++) {
              if(meeting === meetings[i].name){
                  for(var i=0; i < attendees.length; i++){
                      if( attendees[i] == user){
                          attendees.splice(i, 1);
                          }
                    }
                    break;
            //   localStorage.setItem("meetings", JSON.stringify(meetings));
            //   this.componentKey += 1;
             }
            // break;
          }
          localStorage.setItem("meetings", JSON.stringify(meetings));
          this.componentKey += 1;
       },

      deleteMeeting(meetings, meeting)  {
          for (var i = 0; i < meetings.length; i++) {
              if(meeting === meetings[i].name){
                  meetings.splice(i, 1);
              break;
              }
            }
              localStorage.setItem("meetings", JSON.stringify(meetings));
              this.componentKey += 1;
        },
  }
}
</script>