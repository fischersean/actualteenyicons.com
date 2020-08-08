<template>
  <div id="designer">
    <div>
      <div class="slspaced">
        <label>
          R
          <input
            style="--slthumb-color:rgba(219,20,20, 1);"
            type="range"
            min="0"
            max="255"
            class="slider"
            id="redslider"
            v-model="preview_red"
          />
        </label>
      </div>
      <div class="slspaced">
        <label>
          G
          <input
            style="--slthumb-color:rgba(20,219,20, 1);"
            type="range"
            min="0"
            max="255"
            class="slider"
            id="greenslider"
            v-model="preview_green"
          />
        </label>
      </div>
      <div class="slspaced">
        <label>
          B
          <input
            style="--slthumb-color:rgba(20,20,219, 1);"
            type="range"
            min="0"
            max="255"
            class="slider"
            id="blueslider"
            v-model="preview_blue"
          />
        </label>
      </div>
    </div>

    <SVGPreview
      v-bind:r="preview_red"
      v-bind:g="preview_green"
      v-bind:b="preview_blue"
      v-on:copiedData="reemitCp"
    />
  </div>
</template>

<script>
import SVGPreview from './SVGPreview';

export default {
  name: 'Designer',
  components: {
    SVGPreview,
  },
  data: function() {
    return {
      preview_red: (function() {
        return Math.random() * 255;
      })(),
      preview_green: (function() {
        return Math.random() * 255;
      })(),
      preview_blue: (function() {
        return Math.random() * 255;
      })(),
    };
  },
  methods: {
    reemitCp: function() {
      this.$emit('copiedData');
    },
    colorPreview: function() {
      return (
        'fill:rgb(' +
        this.preview_red +
        ',' +
        this.preview_green +
        ',' +
        this.preview_blue +
        ');'
      );
    },
  },
};
</script>

<style>
:root {
  --slthumb-color: rbga(0, 0, 0, 1);
}
#designer {
  margin: auto;
  display: flex;
  flex-diretion: column;
}
.slspaced {
  margin-right: 0.5em;
  margin-top: 1em;
}

/*---------------------------------------------------------------*/
/* The slider itself */
.slider {
  -webkit-appearance: none; /* Override default CSS styles */
  appearance: none;
  height: 0.5em;
  background: #c0c0c0; /* Grey background */
  border-radius: 20px;
  outline: none; /* Remove outline */
  opacity: 0.7; /* Set transparency (for mouse-over effects on hover) */
  -webkit-transition: 0.2s; /* 0.2 seconds transition on hover */
  transition: opacity 0.2s;
}

/* Mouse-over effects */
.slider:hover {
  opacity: 1; /* Fully shown on mouse-over */
}

/* The slider handle (use -webkit- (Chrome, Opera, Safari, Edge) and -moz- (Firefox) to override default look) */
.slider::-webkit-slider-thumb {
  -webkit-appearance: none; /* Override default look */
  appearance: none;
  width: 1.25em; /* Set a specific slider handle width */
  height: 1.25em; /* Slider handle height */
  background: var(--slthumb-color); /* Green background */
  cursor: pointer; /* Cursor on hover */
  border-radius: 100%;
  border-style: solid;
  border-width: thin;
}

.slider::-moz-range-thumb {
  width: 1.25em; /* Set a specific slider handle width */
  height: 1.25em; /* Slider handle height */
  background: var(--slthumb-color); /* Green background */
  cursor: pointer; /* Cursor on hover */
  border-radius: 100%;
  border-style: solid;
  border-width: thin;
}
</style>
