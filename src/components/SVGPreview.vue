<template>
  <div v-on:click="cpDOM" class="previewsvg" :style="cssProps">
    <svg id="svgPixel" width="5" height="5">
      <rect width="5" height="5" />
    </svg>
    <div class="prevLabel">
      <p class="colorVal">
        <b>
          {{ hexRGB() }}
        </b>
      </p>
    </div>
  </div>
</template>

<script>
import copyToClipboard from '@/lib/copyToClipboard.js';
export default {
  name: 'SVGPreview',
  components: {},
  props: ['r', 'g', 'b'],
  data: function() {
    return {};
  },
  methods: {
    hexRGB: function() {
      let toHex = function(a) {
        return parseInt(a).toString(16);
      };
      let _r = toHex(this.r);
      let _g = toHex(this.g);
      let _b = toHex(this.b);
      return '#' + _r + _g + _b;
    },
    cpDOM() {
      // Copy svg html code to clipboard. Browser support is if-y

      var cpSVG = document.createElement('svg');
      cpSVG.setAttribute('width', '1');
      cpSVG.setAttribute('height', '1');
      cpSVG.setAttribute(
        'fill',
        'rgb(' +
          parseInt(this.r) +
          ',' +
          parseInt(this.g) +
          ',' +
          parseInt(this.b) +
          ')',
      );

      var rect = document.createElement('rect');
      rect.setAttribute('width', '1');
      rect.setAttribute('height', '1');

      cpSVG.appendChild(rect);
      var cpTxt = cpSVG.outerHTML;

      console.log(cpTxt + ' Copied to clipboard');

      var success = copyToClipboard(cpTxt);

      if (success) {
        this.$emit('copiedData');
      }
    },
  },
  computed: {
    cssProps() {
      return {
        '--text-color': (function(r, g, b) {
          const brightness = Math.round(
            (parseInt(r) * 299 + parseInt(g) * 587 + parseInt(b) * 114) / 1000,
          );
          const textColor = brightness > 125 ? 'black' : 'white';
          return textColor;
        })(this.r, this.g, this.b),
        '--svgColor': 'rgb(' + this.r + ',' + this.g + ',' + this.b + ')',
      };
    },
  },
};
</script>

<style>
p {
  letter-spacing: 0.1em;
}
svg {
  fill: var(--svgColor);
}
.previewsvg {
  cursor: pointer;
  width: 6em;
  padding-top: 1em;
  border-style: solid;
  border-radius: 10px;
  border-color: var(--svgColor);
  box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.2);
}
.colorVal {
  font-size: medium;
  visibile: var(--visibile);
  text-align: center;
  color: var(--text-color);
  letter-spacing: 0px;
  /*text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,*/
  /*1px 1px 0 #000;*/
}
.prevLabel {
  bottom: 0;
  margin-top: 1.5em;
  padding: 0.1em 0.75em 0.1em 0.75em;
  background-color: var(--svgColor);
}
</style>
