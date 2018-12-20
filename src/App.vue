<template>
  <v-app class="criteo-app">
    <v-layout justify-center>
      <v-content class="main-page">
        <!-- eslint-disable-next-line vue/valid-v-model -->
        <div v-model="stepper"
          class="content-width stepper"
        >
          <div
            v-for="(step, i) in steps"
            class="stepper-step"
            :class="[stepper === i+1 ? 'active' : stepper > i+1 ? 'done' : '']"
            :key="i"
          >
            <span class="stepper-step-number">{{ i + 1 }}</span>
            <span class="stepper-step-name">
              {{step}}
              <span
                class="stepper-step-active"
                v-show="stepper === i + 1"
              ></span>
            </span>
          </div>
        </div>
        <div class="page-title">
          <div class="content-width">
            <h1 class="page-title-main">
              Create an explicit audience
            </h1>
            <h3 class="page-title-subtitle">
              Define an estimation of people you can reach from their interests.
            </h3>
          </div>
        </div>
        <Audience />
        <div class="controls">
          <span class="controls-btn">
            <v-btn flat>Cancel</v-btn>
          </span>
          <span class="controls-btn">
            <v-btn color="#0d6380" depressed dark>Create Audience</v-btn>
          </span>
        </div>
      </v-content>
    </v-layout>
  </v-app>
</template>

<script>
import Audience from './components/Audience/Audience'

export default {
  name: `App`,
  components: {
    Audience
  },
  data () {
    return {
      stepper: 2,
      steps: [`OBJECTIVE`, `AUDIENCE`, `PARAMETERS`, `LAUNCH`]
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Rubik:400,500,700');
@import './assets/scss/variables.scss';

* {
  font-family: 'Rubik', 'Roboto', sans-serif;
}

body, html {
  color: #1d1e1e;
  background-color: $whiteColor;
  box-sizing: border-box;
}

.content-width {
  max-width: 1290px;
  padding: 0 10px;
  margin: auto;
}

.criteo-app.application {
  background-color: $whiteColor;
}

.page-title {
  background-color: $blueColor;
  color: $whiteColor;
  padding: 23px 10px;

  &-main {
    font-size: 32px;
    font-weight: 500;
    line-height: 1;
  }

  &-subtitle {
    font-weight: 400;
    font-size: 14px;
    line-height: 1;
    padding: 7px 0 0 2px;
  }
}

.v-input.app-input {
  background-color: #fff;
  border: 1px solid #676a6a;
  border-radius: 3px;
  box-shadow: none;
  font-size: 14px;

  .v-input__slot {
    box-shadow: none !important;
    padding: 0 9px !important;
    width: calc(100% - 2px);
    min-height: calc(100% - 4px);
  }

  .v-input__control {
    min-height: 34px;
    align-items: center;
    align-content: center;
    justify-content: center;
  }

  &.app-input-small {
    max-width: 250px;
  }
}

.app-title {
  font-weight: 500;
}

.app-label {
  font-weight: 500;
  padding-bottom: 8px;
  display: inline-block;
}

.app-select {
  font-size: 14px;

  .v-input__slot {
    border: 1px solid #676a6a !important;
    border-radius: 3px;
    min-height: 36px !important;
    box-shadow: none !important;
    padding: 0 8px !important;
  }

  .v-text-field .v-input__append-inner {
    padding-left: 2px;
  }
}

.stepper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  padding: 23px 20px;

  &:after {
    content: '';
    position: absolute;
    height: 1px;
    background-color: #cacccd;
    width: calc(100% - 40px);
    top: 50%;
    left: 20px;
    right: 20px;
    z-index: 0;
  }

  &-step {
    display: flex;
    align-items: center;
    background-color: $whiteColor;
    position: relative;
    z-index: 1;
    padding-right: 11px;

    &:last-child {
      padding-right: 0;
    }

    &-number {
      display: flex;
      width: 40px;
      height: 40px;
      border: 3px solid #676a6a;
      color: #676a6a;
      border-radius: 100%;
      align-items: center;
      justify-content: center;
      font-weight: 500;
      font-size: 21px;
    }

    &-name {
      color: #676a6a;
      position: relative;
      padding-left: 5px;
      font-weight: 500;
    }

    &-active {
      border-radius: 100%;
      position: absolute;
      width: 8px;
      height: 8px;
      background-color: #026381;
      bottom: -9px;
      left: 5px;
    }

    &.active {
      .stepper-step-number {
        border-color: #026381;
        color: #026381;
      }
      .stepper-step-name {
        color: #026381;
      }
    }

    &.done {
      .stepper-step-number {
        border-color: #026381;
        background-color: #026381;
        color: #fff;
      }
      .stepper-step-name {
        color: #026381;
      }
    }
  }
}

.controls {
  text-align: center;
  padding: 15px 10px;
  border-top: 1px solid $greyColor;

  &-btn {
    padding-left: 10px;
  }
}
</style>
