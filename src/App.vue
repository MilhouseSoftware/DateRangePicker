<template>
  <div id="app">
    <h1>Date Range Picker</h1>

    <date-range-picker
      v-model="dateRange"
      :locale-data="{ format: 'mm-dd-yyyy HH:MM', separator: ' - ' }"
      :append-to-body="true"
      :ranges="false"
      :captionsOfDate="dateInfoExample"
      :min-date="minDate"
      :opens="opens"
      :time-picker-labels="labels"
      @toggle="onToggle"
      @select="validateRange"
      @update="onUpdate"
    >
      <template v-slot:input="">
        <fg-input
          :value="range"
          :readonly="true"
          addon-left-icon="bx bx-calendar"
          placeholder="Select date"
        />
      </template>
      <div slot="footer" slot-scope="data" class="slot">
        <div class="container-fluid">
          <div v-if="validMsg !== ''" class="date-range-error">
            {{ validMsg }}
          </div>
          <div class="row align-items-center">
            <div class="col-sm-12 text-right">
              <n-button
                type="danger"
                size="sm"
                class="mr-1"
                @click.native="data.clickCancel"
              >
                Cancel
              </n-button>
              <n-button
                :disabled="data.in_selection || validMsg !== ''"
                type="success"
                size="sm"
                @click.native="data.clickApply"
              >
                Apply
              </n-button>
            </div>
          </div>
        </div>
      </div>
    </date-range-picker>
  </div>
</template>
<script>
import DateRangePicker from "./components/DateRangePicker.vue";
export default {
  components: {
    DateRangePicker
  },
  data() {
    return {
      title: "APC DATERANGE PICKER",
      dateRange: {
        startDate: new Date("2023-09-02"),
        endDate: new Date("2023-09-31")
      },
      minDate: new Date("2023-09-01"),
      validMsg: "",
      opens: "right",
      labels: ["Check In Time", "Check Out Time"],
      dateInfoExample: [
        { date: "2023-09-03", price: 1480.9 },
        { date: "2023-09-05", price: 98.7 },
        { date: "2023-09-12", price: 53.9 },
        { date: "2023-09-14", price: 80.0 },
        { date: "2023-09-16", price: 125.4 }
      ]
    };
  },
  methods: {
    validateRange({ startDate, endDate }) {
      console.log("startDate: ", startDate);
      console.log("endDate: ", endDate);
    },
    onUpdate(date) {
      this.$emit("update", date);
    },
    onToggle(open) {
      if (!open) {
        this.validMsg = "";
      } else {
        this.$emit("scrollUp");
      }
    }
  }
};
</script>
<style lang="scss" scoped>
@import "assets/daterangepicker.scss";
::v-deep {
  .form-control {
    padding-left: 12px !important;
    padding-right: 8px !important;
  }
}
.date-range-error {
  color: #ff3636 !important;
  text-align: center;
}
</style>
