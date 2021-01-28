<template>
  <div class="calendar-component-wrapper">
    <h1 class="header">Monthly Data</h1>
    <div class="graphs-wrapper">
      <div class="graph">
        <calendar-chart
          v-if="passdata"
          v-bind:dateData="calendarOptions.events"
          :height="375"
          :width="850"
        />
      </div>
      <div class="graph">
        <ratings-chart
          v-if="passdata"
          v-bind:ratingsArray="ratingsArray"
          :height="375"
          :width="850"
        />
        <p class="note">
          Hover over data points for precise corresponding values.
        </p>
      </div>
    </div>
    <h1 class="header">Interactive Calendar</h1>
    <div class="calendar-wrapper">
      <full-calendar :options="calendarOptions" />
    </div>
    <p class="note">
      Click on the arrow keys on the right-top corner of the calendar to change
      months and click on "+# more" for full list of movie releases for that
      date.
    </p>
  </div>
</template>

<script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import CalendarChart from "./CalendarChart.vue";
import RatingsChart from "./RatingsChart.vue";

export default {
  components: {
    FullCalendar,
    CalendarChart,
    RatingsChart,
  },
  props: ["filmdata", "yearInput"],
  data() {
    return {
      passdata: false,
      ratingsArray: [[], [], [], [], [], [], [], [], [], [], [], []],
      calendarOptions: {
        plugins: [dayGridPlugin],
        initialView: "dayGridMonth",
        initialDate: new Date(`${this.yearInput}-01-02`),
        fixedWeekCount: false,
        dayMaxEventRows: true,
        events: [],
        eventColor: "#c40a2f",
        headerToolbar: {
          start: "title",
          center: "",
          end: "prev,next",
        },
        height: "100%",
      },
    };
  },

  mounted() {
    for (let i = 0; i < this.filmdata.length; i++) {
      for (let j = 0; j < this.filmdata[i].length; j++) {
        this.calendarOptions.events.push({
          title: this.filmdata[i][j].original_title,
          date: this.filmdata[i][j].release_date,
        });
        for (let z = 0; z < 12; z++) {
          if (new Date(this.filmdata[i][j].release_date).getMonth() === z) {
            this.ratingsArray[z].push(this.filmdata[i][j].vote_average);
          }
        }
      }
    }
    console.log(this.ratingsArray);
    this.passdata = true;
  },
};
</script>

<style>
.calendar-component-wrapper {
  padding-top: 10px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-image: linear-gradient(rgb(236, 236, 236), rgb(148, 148, 148));
}

.calendar-wrapper {
  padding-top: 20px;
  width: 90%;
  height: 750px;
  max-width: 1000px;
}
.graphs-wrapper {
  height: 100%;
  width: 90%;
  max-width: 1000px;
}

.graph {
  padding-bottom: 40px;
}

.fc .fc-toolbar-title {
  color: yellow;
}

.fc .fc-daygrid-day-number {
  font-size: 18px;
  color: rgb(230, 255, 5);
  font-weight: 500;
}

.fc .fc-button-primary {
  background-color: #c40a2f;
}

.fc .fc-button {
  line-height: 0.5;
  font-size: 0.75em;
}

.fc-theme-standard .fc-scrollgrid {
  border-color: yellow;
}

.fc-theme-standard td {
  border: solid 1px rgb(255, 255, 0);
}
.fc-theme-standard th {
  border: solid 1px rgb(255, 255, 0);
  background-color: #5f5f5f;
}
.fc .fc-col-header-cell-cushion {
  font-size: 16px;
  color: rgb(252, 252, 252);
}

@media only screen and (max-width: 600px) {
  .calendar-wrapper {
    padding-top: 20px;
    width: 100%;
    height: 600px;
    width: 95%;
    font-size: 10px;
  }
  .fc .fc-button {
    line-height: 0.5;
    font-size: 1.25em;
  }
}
</style>
