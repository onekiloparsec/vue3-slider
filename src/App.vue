<template>
  <section class="controls" :class="{ expand }">
    <h1>Controls</h1>
    <div class="seperator"></div>

    <div v-show="showInputs" class="inputs">
      <div class="item">
        <h2>height:</h2>
        <power-slider
          class="slider"
          v-model="height"
          tooltip
          :min="5"
          :height="8"
          trackColor="rgba(0,0,0,0.15)"
          color="#005CC8"
          tooltipColor="black"
          tooltipTextColor="white"
          tooltipText="%vpx"
        />
      </div>

      <div class="item">
        <h2>width:</h2>
        <power-slider
          class="slider"
          v-model="width"
          tooltip
          :height="8"
          :min="70"
          :max="650"
          trackColor="rgba(0,0,0,0.15)"
          color="#005CC8"
          tooltipColor="black"
          tooltipTextColor="white"
          tooltipText="%vpx"
        />
      </div>

      <div class="item">
        <h2>min:</h2>
        <power-slider
          class="slider"
          v-model="min"
          tooltip
          :height="8"
          :min="-1000"
          :max="1000"
          trackColor="rgba(0,0,0,0.15)"
          color="#005CC8"
          tooltipColor="black"
          tooltipTextColor="white"
        />
      </div>

      <div class="item">
        <h2>max:</h2>
        <power-slider
          class="slider"
          v-model="max"
          tooltip
          :height="8"
          :min="-1000"
          :max="1000"
          trackColor="rgba(0,0,0,0.15)"
          color="#005CC8"
          tooltipColor="black"
          tooltipTextColor="white"
        />
      </div>

      <div class="item">
        <h2>step:</h2>
        <power-slider
          class="slider"
          v-model="step"
          tooltip
          :height="8"
          :min="0"
          :max="50"
          :step="0.1"
          trackColor="rgba(0,0,0,0.15)"
          color="#005CC8"
          tooltipColor="black"
          tooltipTextColor="white"
        />
      </div>

      <div class="item">
        <h2>tooltip:</h2>
        <input type="checkbox" name="tooltip" v-model="tooltip"/>
      </div>

      <div class="item">
        <h2>tooltipText:</h2>
        <input type="text" name="tooltipText" v-model="tooltipText"/>
      </div>

      <div class="item">
        <h2>orientation:</h2>
        <select name="orientation" v-model="orientation">
          <option value="horizontal">horizontal</option>
          <option value="vertical">vertical</option>
          <option value="circular">circular</option>
        </select>
      </div>

      <div class="item">
        <h2>rainbow:</h2>
        <input type="checkbox" name="colorShift" v-model="colorShift"/>
      </div>

      <button @click="sliderVal += 10">Add 10 to slider value</button>
      <button @click="sliderVal -= 10">Minus 10 from slider value</button>
    </div>

    <button class="grow-btn" @click="openControls">
      {{ !expand ? 'open' : 'close' }}
    </button>
  </section>

  <power-slider
    class="slider"
    :class="{ colorShift }"
    v-model="sliderVal"
    :height="height"
    tooltip="always"
    :width="width + 'px'"
    :repeat="false"
    :min="min"
    :max="max"
    :step="step"
    :tooltip-text="tooltipText"
    handle-color="red"
    handle-border-color="green"
    :handle-scale="1.4"
    color="transparent"
    :orientation="orientation"
  >
    <template #track>
      <div style="background-color: blue; width: 100%; height: 0.1em;"></div>
    </template>
  </power-slider>
  <h1>{{ sliderVal }}</h1>
</template>

<script lang="ts">
  import { defineComponent } from "vue";
  import PowerSlider from "./components/power-slider.vue";

  export default defineComponent({
    name: "ServeDev",
    components: {
      PowerSlider,
    },
    data () {
      return {
        sliderVal: 30,
        expand: false,
        showInputs: false,
        height: 10,
        width: 200,
        min: 0,
        max: 100,
        step: 1,
        tooltip: 'always',
        tooltipText: "%v",
        orientation: "horizontal",
        colorShift: false,
        sticky: false,
        repeat: false,
        flip: false,
        circleOffset: 0,
      };
    },
    methods: {
      openControls () {
        if (!this.expand) {
          this.showInputs = true;
        } else {
          setTimeout(() => (this.showInputs = false), 300);
        }

        setTimeout(() => (this.expand = !this.expand), 10);
      },
    },
  });
</script>

<style>
  body {
    width: 100%;
    height: 100vh;
    /*background-color: #080a0d;*/
    margin: 0;
    padding: 8%;
    box-sizing: border-box;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  }

  #app {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    height: 100%;
  }

  h1 {
    color: rgba(255, 255, 255, 0.8);
  }

  .controls {
    z-index: 10;
    position: absolute;
    top: 1rem;
    right: 1rem;
    width: 15rem;
    padding: 1.2rem;
    background-color: #fff;
    border-radius: 0.6rem;
    transition: width 0.3s ease;
    overflow: hidden;
  }

  .controls.expand {
    width: 22rem;
  }

  .controls.expand .inputs {
    height: 515px;
    opacity: 1;
  }

  .controls .inputs {
    margin-bottom: 0.5rem;
    height: 0;
    opacity: 0;
    transition: height 0.3s ease, opacity 0.3s ease;
  }

  .controls .inputs h2 {
    padding-right: 0.8rem;
    margin: 0;
    font-size: 0;
  }

  .controls.expand .inputs h2 {
    padding-right: 0.8rem;
    margin: 0;
    font-size: 1.1rem;
  }

  .controls .inputs .item {
    display: flex;
    align-items: center;
    padding: 0.4rem 0;
  }

  .controls h1 {
    color: black;
    font-size: 1.3rem;
    margin: 0;
  }

  .seperator {
    width: 100%;
    height: 2px;
    background-color: black;
    margin: 0.6rem 0;
  }

  .controls .grow-btn {
    width: 100%;
    padding: 0.5rem;
    font-size: 1rem;
    font-weight: 600;
    /*background-color: black;*/
    color: white;
    border: none;
    border-radius: 0.4rem;
    outline: none;
    cursor: pointer;
  }

  .colorShift {
    animation: color-shift linear 20s;
    animation-iteration-count: infinite;
  }

  @keyframes color-shift {
    0% {
      filter: hue-rotate(0deg);
    }

    50% {
      filter: hue-rotate(360deg);
    }

    100% {
      filter: hue-rotate(0deg);
    }
  }
</style>

