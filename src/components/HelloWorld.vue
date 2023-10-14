<script>
import { defineComponent } from 'vue'
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import timeGridPlugin from '@fullcalendar/timegrid'
import interactionPlugin from '@fullcalendar/interaction'
import { INITIAL_EVENTS, createEventId } from './event-utils'
import SideBar from './SideBar.vue'
import 'bootstrap/dist/css/bootstrap.css';


export default defineComponent({
  components: {
    FullCalendar,
    SideBar
  },
  data() {
    return {
      selectedOption: null,
      calendarOptions: {
        plugins: [
          dayGridPlugin,
          timeGridPlugin,
          interactionPlugin 
        ],

        headerToolbar: {
          right: 'prev,next, timeGridWeek,timeGridDay',
          center: 'title',
          left: ''
        },
        initialView: 'timeGridWeek',
        initialEvents: INITIAL_EVENTS, 
        editable: true,
        selectable: true,
        selectMirror: true,
        dayMaxEvents: true,
        weekends: true,
        isCalendarVisible: false,
        select: this.handleDateSelect,
        eventClick: this.handleEventClick,
        eventsSet: this.handleEvents
        /* update a remote database when these fire:
        eventAdd:
        eventChange:
        eventRemove:
        */
      },
      currentEvents: [],
    }
  },
  methods: {
    handleItemClick(option) {
      this.selectedOption = option;
    },
    handleWeekendsToggle() {
      this.calendarOptions.weekends = !this.calendarOptions.weekends // update a property
    },
    handleDateSelect(selectInfo) {
      let title = prompt('Please enter a new title for your event')
      let calendarApi = selectInfo.view.calendar

      calendarApi.unselect() 

      if (title) {
        calendarApi.addEvent({
          id: createEventId(),
          title,
          start: selectInfo.startStr,
          end: selectInfo.endStr,
          allDay: selectInfo.allDay
        })
      }
    },
    handleEventClick(clickInfo) {
      if (confirm(`Are you sure you want to delete the event '${clickInfo.event.title}'`)) {
        clickInfo.event.remove()
      }
    },
    handleEvents(events) {
      this.currentEvents = events
    },
    toggleCalendar() {
      this.isCalendarVisible = !this.isCalendarVisible;
    },
  }
})

</script>

<template>
  <div class='demo-app'>
    <v-app :style="{ background: $veutify, theme, dark, background }">
      <SideBar />
    </v-app>
  </div>

  <div class='demo-app-main'>
    <h2 class="title">Content Calender</h2>

    <div class="sides">

      <div id="" class="dropdown">
        <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown"
          aria-haspopup="true" aria-expanded="false">
          5 Accounts
        </button>
        <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
          <a class="dropdown-item" href="#">Account 1</a>
          <a class="dropdown-item" href="#">Account 2</a>
          <a class="dropdown-item" href="#">Account 3</a>
        </div>
      </div>
      <div class="dropdown">
        <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown"
          aria-haspopup="true" aria-expanded="false">
          All Statuses
        </button>
        <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
          <a class="dropdown-item" href="#">Status 1</a>
          <a class="dropdown-item" href="#">Status 2</a>
          <a class="dropdown-item" href="#">Status 3</a>
        </div>
      </div>
    </div>
    <FullCalendar class='demo-app-calendar' :options='calendarOptions'>
      <template v-slot:eventContent='arg'>
        <b>{{ arg.timeText }}</b>
        <i>{{ arg.event.title }}</i>
      </template>
    </FullCalendar>
  </div>
</template>

<style lang='css'>
.title {
  padding-left: 5px;
  padding-bottom: 0px;
  text-align: left;
  font-size: 20px;
  font-weight: 700;
  transform: translateY(20px);
}

.sides {
  display: flex;
  flex-direction: row;

  transform: translateY(40px);
}

.dropdown {
  padding-left: 10px;
}

h2 {
  margin: 0;
  font-size: 16px;
}

ul {
  margin: 0;
  padding: 0 0 0 1.5em;
}

li {
  margin: 1.5em 0;
  padding: 0;
}

b {
  margin-right: 3px;
  
}

body #app {
  display: flex;
  margin-top: 0px;
}

.demo-app-main {
  flex-grow: 1;
  padding-left: 100px;
  height: 700px;
  padding-right: 0px;
  width: 1000px;
}

.fc {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
