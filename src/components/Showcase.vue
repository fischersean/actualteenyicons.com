<template>
  <div>
    <div id="title" class="sticky">
      <h2>
        Gallery
      </h2>
    </div>
    <div id="svggrid">
      <div v-for="(item, index) in totalIter" v-bind:key="index">
        <SVGPreview
          class="pelem"
          :r="item[0]"
          :g="item[1]"
          :b="item[2]"
          v-on:copiedData="reemitCp"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SVGPreview from './SVGPreview';
export default {
  name: 'Showcase',
  components: {
    SVGPreview,
  },
  props: [],
  data: function() {
    return {
      count: 5,
      totalIter: [],
    };
  },
  methods: {
    reemitCp: function() {
      this.$emit('copiedData');
    },
  },
  mounted() {},
  created() {
    // Create random colors
    let tmp = [];
    for (let j = 0; j < 3; j++) {
      tmp.push([]);
      for (let i = 0; i < this.count; i++) {
        tmp[j].push(Math.random() * 255);
      }
    }

    // This isnt very good but it almost definately is good <i> enough </>
    for (let r = 0; r < this.count; r++) {
      for (let g = 0; g < this.count; g++) {
        for (let b = 0; b < this.count; b++) {
          this.totalIter.push([tmp[0][r], tmp[1][g], tmp[2][b]]);
        }
      }
    }
  },
};
</script>

<style>
h2 {
  border-style: solid;
  border-color: black;
  box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.3);
  margin: auto;
  border-radius: 5px;
}
#title {
  background: white;
  margin-top: 1.5em;
  margin-bottom: 1.5em;
  padding-top: 0.1em;
  padding-bottom: 0;
  font-size: xx-large;
}
#svggrid {
  display: grid;
  grid-gap: 2em;
  grid-template-columns: repeat(auto-fill, minmax(6em, 1fr));
  max-width: 45em;
  margin: auto;
}

@media (min-width: 700px) {
  h2 {
    padding-right: 5em;
    padding-left: 5em;
    max-width: 5em;
  }
}

.pelem {
  margin: 0 auto;
}
.sticky {
  position: -webkit-sticky; /* Safari */
  position: sticky;
  top: 0em;
}
</style>
