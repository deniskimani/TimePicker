<template>
  <div class="time-picker">
    <div class="input-group">
      <input
        type="text"
        id="time-picker-input"
        class="form-control"
        @focus="inputFocused"
        @focusout="inputOut"
        v-model="selected_time"
      />
      <span class="input-group-addon" @click="inputFocused">
        <span class="fa fa-clock-o" aria-hidden="true"></span>
      </span>
      <div class="pop-up time-picker-pop-up" :id="popup_id">
        <table>
          <tbody>
            <tr>
              <td width="25%">
                <a href="#" @click.prevent="addHour">
                  <i class="fa fa-chevron-up" aria-hidden="true"></i>
                </a>
              </td>
              <td width="25%"></td>
              <td width="25%">
                <a href="#" @click.prevent="addMinute">
                  <i class="fa fa-chevron-up" aria-hidden="true"></i>
                </a>
              </td>
              <td width="25%"></td>
            </tr>
            <tr height="100px">
              <td>
                <strong class="bold">{{ hour }}</strong>
              </td>
              <td>
                <span class="text-muted">:</span>
              </td>
              <td>
                <strong class="bold">{{ minute }}</strong>
              </td>
              <td>
                <a href="#" @click.prevent="togglePeriod" class="btn btn-primary">{{ period }}</a>
              </td>
            </tr>
            <tr>
              <td>
                <a href="#" @click.prevent="subHour">
                  <i class="fa fa-chevron-down" aria-hidden="true"></i>
                </a>
              </td>
              <td></td>
              <td>
                <a href="#" @click.prevent="subMinute">
                  <i class="fa fa-chevron-down" aria-hidden="true"></i>
                </a>
              </td>
              <td></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hour: 12,
      minute: "00",
      period: "PM",
      selected_time: this.value,
      popup_id: this.generateRandomString(10)
    };
  },

  props: {
    value: {
      required: true,
      type: String
    }
  },

  methods: {
    inputFocused() {
      document.getElementById(this.popup_id).classList.add("show");
    },

    inputOut(event) {
      document.getElementById(this.popup_id).classList.remove("show"); 
    },

    addHour() {
      if (this.hour == 12) {
        this.hour = 1;
      } else {
        this.hour += 1;
      }
    },

    addMinute() {
      if (this.minute == 55) {
        this.minute = "00";
      } else {
        let min = parseInt(this.minute) + 5;

        if (min < 10) {
          this.minute = `0${min}`;
        } else {
          this.minute = min;
        }
      }
    },

    subHour() {
      if (this.hour == 1) {
        this.hour = 12;
      } else {
        this.hour -= 1;
      }
    },

    subMinute() {
      if (this.minute == "00") {
        this.minute = 55;
      } else {
        let min = parseInt(this.minute) - 5;

        if (min < 10) {
          this.minute = `0${min}`;
        } else {
          this.minute = min;
        }
      }
    },

    togglePeriod() {
      if (this.period == "AM") {
        this.period = "PM";
      } else {
        this.period = "AM";
      }
    },

    generateRandomString(length) {
      var text = "";
      var possible =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

      for (var i = 0; i < length; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length));

      return text;
    }
  },

  watch: {
    hour() {
      this.selected_time = `${this.hour} : ${this.minute} ${this.period}`;
    },

    minute() {
      this.selected_time = `${this.hour} : ${this.minute} ${this.period}`;
    },

    period() {
      this.selected_time = `${this.hour} : ${this.minute} ${this.period}`;
    },

    selected_time() {
      this.$emit("input", this.selected_time);
    }
  }
};
</script>

<style lang='scss' scoped>
.time-picker-pop-up {
  display: none;

  &:hover {
    display: block;
  }

  &.show {
    display: block;
  }
}

.time-picker {
  .pop-up {
    position: absolute;
    left: 0;
    width: 88%;
    z-index: 9;
    top: 50px;
    background: #fff;
    padding: 40px 20px;
    border: 1px solid #ddd;
    box-shadow: 0px 1px 5px #aaa;

    table {
      width: 100%;
      text-align: center;

      .bold {
        font-size: 20px;
        font-weight: 800;
        font-family: monospace;
      }
    }
  }
}
</style>