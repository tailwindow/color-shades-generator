<template>
  <div class="flex bg-gray-300 min-h-screen justify-center">
    <div class="flex flex-col px-4 py-4 bg-gray-100 w-full justify-between max-w-screen-xl shadow-xl">
      <div class="flex flex-col sm:flex-row justify-between mx-4 my-2 items-center">
        <div class="flex flex-col">
          <svg class="h-12" viewBox="0 0 3378 699" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <g id="Tailwindow-Logo" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
              <g id="Tailwindow">
                <g id="Tailwind-Icon" transform="translate(0.000000, 98.000000)">
                  <g id="Icon">
                    <rect id="Rectangle" fill="#709D3D" x="0" y="0" width="512" height="512" rx="64" />
                    <rect id="Rectangle" fill="#FFFFFF" x="149" y="176" width="220" height="220" />
                    <circle id="Oval" fill="#FFFFFF" cx="259" cy="156" r="40" />
                    <circle id="Oval" fill="#709D3D" cx="369" cy="286" r="40" />
                  </g>
                </g>
                <text id="Tailwindow" font-family="Nunito-Bold, Nunito" font-size="512" font-weight="bold" fill="#000000">
                  <tspan x="654" y="518">Tailwindow</tspan>
                </text>
              </g>
            </g>
          </svg>
          <p class="text-xs text-right uppercase -my-2">
            Color shades generator
          </p>
        </div>
        <div class="mt-8 sm:mt-0">
          <label for="regular" class="text-xs leading-7 text-gray-700 font-bold uppercase">Color Interval</label>
          <input id="regular" v-model="colorInterval" type="text" class="shadow w-full border bg-gray-200 border-gray-400 py-1 px-4 text-gray-700 text-md focus:outline-none focus:border-gray-500" placeholder="Regular input text">
        </div>
      </div>
      <hr class="border-gray-400 mx-4 mt-4">
      <div class="flex w-full sm:flex-row flex-wrap justify-center">
        <div v-for="(color, index) in colors" :key="color" class="px-4 w-1/2 sm:w-1/3 md:w-1/4">
          <div class="flex mt-8 mb-4">
            <div class="shadow-md w-8 text-center text-xs py-2 bg-gray-300">
              #
            </div>
            <input
              id="color"
              :value="color"
              type="text"
              class="shadow-md bg-gray-200 w-full text-sm p-2 outline-none"
              name="color"
              placeholder="HEX COLOR"
              @keyup.enter="updateColor($event, index)"
            >
          </div>
          <div class="flex flex-col mb-8">
            <div
              v-for="shade in colorShades[index]"
              :key="shade"
              class="shadow-md focus:outline-none"
              :class="{ 'text-white' : !isLumaLight(shade) }"
              :style="{ backgroundColor: '#' + shade }"
            >
              <p class="text-md py-4 px-4 select-all text-center uppercase opacity-0 hover:opacity-75">
                #{{ shade }}
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="mx-4">
        &nbsp;
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      colors: ['3366FF', '7FED25', '2AC4FC', 'FF5028'],
      colorInterval: 0.18, // percentage
      colorShades: []
    }
  },
  watch: {
    colorInterval () {
      this.colors.forEach((color, index) => {
        this.createTintsAndShades(color, index)
      })
    }
  },
  created () {
    this.colors.forEach((color, index) => {
      this.createTintsAndShades(color, index)
    })
  },
  methods: {
    updateColor (e, index) {
      this.createTintsAndShades(e.target.value, index)
      this.colors[index] = e.target.value
    },
    isLumaLight (color) {
      var c = color.replace('#', '')
      var rgb = parseInt(c, 16) // convert rrggbb to decimal
      var r = (rgb >> 16) & 0xff // extract red
      var g = (rgb >> 8) & 0xff // extract green
      var b = (rgb >> 0) & 0xff // extract blue
      var luma = 0.2126 * r + 0.7152 * g + 0.0722 * b
      if (luma < 110) {
        return false
      }
      return true
    },
    pad (number, length) {
      var str = '' + number
      while (str.length < length) {
        str = '0' + str
      }
      return str
    },
    hexToRGB (colorValue) {
      colorValue = colorValue.toString()
      return {
        red: parseInt(colorValue.substr(0, 2), 16),
        green: parseInt(colorValue.substr(2, 2), 16),
        blue: parseInt(colorValue.substr(4, 2), 16)
      }
    },
    intToHex (rgbint) {
      return this.pad(Math.min(Math.max(Math.round(rgbint), 0), 255).toString(16), 2)
    },
    rgbToHex (rgb) {
      return this.intToHex(rgb.red) + this.intToHex(rgb.green) + this.intToHex(rgb.blue)
    },
    rgbShade (rgb, i) {
      return {
        red: rgb.red * (1 - this.colorInterval * i),
        green: rgb.green * (1 - this.colorInterval * i),
        blue: rgb.blue * (1 - this.colorInterval * i)
      }
    },
    rgbTint (rgb, i) {
      return {
        red: rgb.red + (255 - rgb.red) * i * this.colorInterval,
        green: rgb.green + (255 - rgb.green) * i * this.colorInterval,
        blue: rgb.blue + (255 - rgb.blue) * i * this.colorInterval
      }
    },
    calculateShades (colorValue) {
      return this.calculate(colorValue, this.rgbShade)
    },
    calculateTints (colorValue) {
      return this.calculate(colorValue, this.rgbTint)
    },
    calculate (colorValue, shadeOrTint) {
      var color = this.hexToRGB(colorValue)
      var shadeValues = []
      for (var i = 1; i < 5; i++) {
        shadeValues[i - 1] = this.rgbToHex(shadeOrTint(color, i))
      }
      return shadeValues
    },
    createTintsAndShades (color, index) {
      if (color !== null) {
        // trim hash tag
        color = color.replace('#', '')
        var calculatedShades = this.calculateShades(color)
        var calculatedTints = this.calculateTints(color)
        var result = calculatedTints.reverse().concat(color).concat(calculatedShades)
        this.$set(this.colorShades, index, result)
      }
    }
  }
}
</script>
