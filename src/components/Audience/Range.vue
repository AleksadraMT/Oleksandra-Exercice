<template>
<v-layout>
  <div class="range">
    <div class="range-title">
      Estimated audience size
    </div>
    <v-divider class="range-divider"></v-divider>
    <div>
      <div class="range-current-number">
        {{ currentNumber }}
      </div>
      <div class="range-slider">
        <div
          class="range-slider-filled"
          :style="{left: left + '%', right: right + '%'}"
        >
          <div
            class="range-pin"
            :style="{left: pinleft}"
          ></div>
        </div>
      </div>
      <div class="range-description">
          <span>Low</span><span>High</span>
        </div>
    </div>
    <v-divider class="range-divider"></v-divider>
    <div class="range-about">
      Hints and help text goes here. For example, we can tell here the 
      problem with too big or too specific audience size.
    </div>
  </div>
</v-layout>
</template>

<script>
export default {
  name: 'range',
  created: function() {
    this.current = 15000000;
  },
  data: () => ({
    min: 1000000,
    max: 100000000,
    current: 0,
    calibration: 10,
  }),

  computed: {
    currentNumber: function() {
      return this.current.toString().replace(/(\d)(?=(\d\d\d)+([^\d]|$))/g, '$1 ');
    },
    general: function() {
      return this.min + this.max;
    },
    left: function() {
      return ((100 / this.general) * this.min) + this.calibration;
    },
    right: function() {
      return ((100 / this.general) * (this.general - this.max)) + this.calibration;
    },
    pinleft: function() {
      switch (true) {
        case (this.current === this.min):
          return `-2px`;

        case (this.current === this.max):
          return `calc(100% - 2px)`;

        case (this.current < this.min):
          return -this.left - 2 + (this.left / this.min * this.current) + '%';

        case (this.current > this.min && this.current < this.max):
          return (100 / (this.max - this.min) * this.current) + '%';

        case (this.current > this.max && this.current < this.general):
          return 100 + (this.right / this.min * (this.current - this.max)) + '%';

          case (this.current > this.general):
          return 100 + this.right + '%';
      }
    }
  }
}
</script>

<style lang="scss">
  @import './../../assets/scss/variables.scss';

  .range {
    width: 365px;
    min-height: 295px;
    padding: 20px 40px;
    color: $fontColor;
    background-color: #fff;
    box-shadow: 0 0 7px 1px rgba(0, 0, 0, .1);
    border-radius: 5px;
    position: relative;

    &-title {
      text-align: center;
      line-height: 1;
      font: {
        weight: 700;
        size: 19px;
      }
    }

    &-divider {
      &.v-divider {
        border-color: $greyColor;
        margin: 18px 0;
      }
    }

    &-current-number {
      text-align: center;
      font-weight: 700;
      color: $blueColor;
      font-size: 23px;
      line-height: 1;
      padding: 5px 0 6px;
    }

    &-slider {
      width: 100%;
      height: 8px;
      margin-top: 18px;
      background-color: $greyColor;
      border-radius: 10px;
      position: relative;

      &-filled {
        position: absolute;
        height: 100%;
        background-color: $blueColor;
        top: 0;
        bottom: 0;
        right: 1px;
        left: 1px;
        border-left: 1px solid #fff;
        border-right: 1px solid #fff;
      }
    }

    &-pin {
      width: 6px;
      height: 6px;
      background-color: #c1c4c5;
      position: absolute;
      border-radius: 100%;
      top: -14px;

      &:after {
        content: '';
        position: absolute;
        border-left: 3px solid transparent;
        border-right: 3px solid transparent;
        border-top: 11px solid #c1c4c5;
        top: 3px;
      }
    }

    &-description {
      display: flex;
      justify-content: space-between;
      padding: 7px 0 0 2px;
      font-size: 15px;
      color: #676a6a;
    }

    &-about {
      color: #252626;
      text-align: center;
      line-height: 17px;
      font-size: 14px;
      padding-top: 2px;
    }
  }
</style>
