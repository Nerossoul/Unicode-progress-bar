<template>
  <div class="container">
    <input class="slider" type="range" id="cowbell" name="cowbell" 
         min="0" max="100" value="0" step="1" v-model="per_cent">
    <br>
    <h2>Per cent: {{ per_cent }}</h2>
    <input class="slider" type="range" id="cowbell" name="cowbell" 
         min="2" max="40" value="2" step="1" v-model="bars">
    <br>
    <h2>Progress bar size: {{ bars }}</h2>
    <select v-model="bar_string">
      <option disabled value="">Choose style</option>
      <option v-for="bar_style of bar_styles" :key="bar_style.id">{{ bar_style }}</option>
    </select>
    <input type="text" v-model="bar_string" >
    <h1>{{ result }}{{ per_cent }}%</h1>
  </div>
</template>

<script>
export default {
  name: 'ProgressBar',
  props: {
    msg: String
  },
  data() {
    return {
      per_cent: 0,
      bar_string:'▁▂▃▄▅▆▇█',
      bars: 7,
      bar_styles :[
                    '▁▂▃▄▅▆▇█',
                    '⣀⣄⣤⣦⣶⣷⣿',
                    '⣀⣄⣆⣇⣧⣷⣿',
                    '○◔◐◕⬤',
                    '□◱◧▣■',
                    '□◱▨▩■',
                    '□◱▥▦■',
                    '░▒▓█',
                    '░█',
                    '⬜⬛',
                    '▱▰',
                    '▭◼',
                    '▯▮',
                    '◯⬤',
                    '⚪⚫',
                  ]
    }
  },
  computed: {
    result() {
      return this.get_prog_bar_string(this.bar_string, this.per_cent, this.bars, ' ')
    }
  },
  methods : {
    get_prog_bar_string(bar_string, per_cent, bars, sep = ' ') {
      let result_bar_string = ''
      let bar_weight = 100 / bars
      let full_bars = Math.floor(per_cent / bar_weight)
      let bar_part = (per_cent / bar_weight) - Math.floor(per_cent / bar_weight)
      let part_max = Math.round(1/((1 / bar_weight) - Math.floor(1 / bar_weight)))

      for (let i = 1; i<= full_bars; i++) {
        result_bar_string += bar_string[bar_string.length - 1] + sep
      }
      if (bar_part != 0) {
        let current_parts = bar_part / (1 / part_max)
        let part_char_index = Math.round(((bar_string.length-1) / part_max * current_parts )) 
        result_bar_string += bar_string[part_char_index] + sep

        full_bars +=1
      }
      for (let i = full_bars; i< bars; i++) {
        result_bar_string += bar_string[0] + sep
      }
      return  result_bar_string
    }
  }
}
</script>

<style scoped>
.container {
  width: 100%
}

select {
  height: 38px;
  padding: 4px;
  font-size: 15px;
}
input[type=text],[type=number] {
  -webkit-appearance: none;
  width: 45%;
  height: 30px;
  margin: 4px 0;
  padding: 4px;
  font-size: 15px;
}
input[type=range].slider {
  -webkit-appearance: none;
  width: 90%;
  margin: 4px 0;
}
input[type=range].slider:focus {
  outline: none;
}
input[type=range].slider::-webkit-slider-runnable-track {
  width: 90%;
  height: 32px;
  cursor: pointer;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  background: #ffffd6;
  border-radius: 0px;
  border: 0px solid #010101;
}
input[type=range].slider::-webkit-slider-thumb {
  box-shadow: 0.8px 0.8px 1.9px rgba(0, 0, 62, 0.67), 0px 0px 0.8px rgba(0, 0, 88, 0.67);
  border: 0px solid rgba(124, 124, 2, 0.57);
  height: 40px;
  width: 14px;
  border-radius: 4px;
  background: #3871a9;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -4px;
}
input[type=range].slider:focus::-webkit-slider-runnable-track {
  background: #ffffff;
}
input[type=range].slider::-moz-range-track {
  width: 90%;
  height: 32px;
  cursor: pointer;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  background: #ffffd6;
  border-radius: 0px;
  border: 0px solid #010101;
}
input[type=range].slider::-moz-range-thumb {
  box-shadow: 0.8px 0.8px 1.9px rgba(0, 0, 62, 0.67), 0px 0px 0.8px rgba(0, 0, 88, 0.67);
  border: 0px solid rgba(124, 124, 2, 0.57);
  height: 40px;
  width: 14px;
  border-radius: 4px;
  background: #3871a9;
  cursor: pointer;
}
input[type=range].slider::-ms-track {
  width: 90%;
  height: 32px;
  cursor: pointer;
  background: transparent;
  border-color: transparent;
  color: transparent;
}
input[type=range].slider::-ms-fill-lower {
  background: #ffff24;
  border: 0px solid #010101;
  border-radius: 0px;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}
input[type=range].slider::-ms-fill-upper {
  background: #ffffd6;
  border: 0px solid #010101;
  border-radius: 0px;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}
input[type=range].slider::-ms-thumb {
  box-shadow: 0.8px 0.8px 1.9px rgba(0, 0, 62, 0.67), 0px 0px 0.8px rgba(0, 0, 88, 0.67);
  border: 0px solid rgba(124, 124, 2, 0.57);
  height: 40px;
  width: 14px;
  border-radius: 4px;
  background: #3871a9;
  cursor: pointer;
  height: 32px;
}
input[type=range].slider:focus::-ms-fill-lower {
  background: #ffffd6;
}
input[type=range].slider:focus::-ms-fill-upper {
  background: #ffffff;
}

</style>
