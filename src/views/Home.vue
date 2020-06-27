<template>
  <div class="flex bg-gray-300 min-h-screen justify-center">
    <div class="flex flex-col px-4 py-4 bg-gray-100 w-full justify-between max-w-screen-xl shadow-xl">
      <div class="flex flex-col sm:flex-row justify-between mx-4 my-2 items-center">
        <div class="flex flex-col mr-4">
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
        <div class="flex mt-8 sm:mt-0">
          <div class="flex items-end mr-4 text-center">
            <a class="bg-gray-300 shadow-md rounded-full w-10 h-10 mr-4 p-2 flex items-center" href="javascript:void(0)">
              <svg class="fill-current flex-1 text-gray-700" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512"><path d="M572.52 241.4C518.29 135.59 410.93 64 288 64S57.68 135.64 3.48 241.41a32.35 32.35 0 0 0 0 29.19C57.71 376.41 165.07 448 288 448s230.32-71.64 284.52-177.41a32.35 32.35 0 0 0 0-29.19zM288 400a144 144 0 1 1 144-144 143.93 143.93 0 0 1-144 144zm0-240a95.31 95.31 0 0 0-25.31 3.79 47.85 47.85 0 0 1-66.9 66.9A95.78 95.78 0 1 0 288 160z" /></svg>
            </a>
            <a class="bg-gray-300 shadow-md rounded-full w-10 h-10 mr-2 p-2 flex items-center" href="javascript:void(0)">
              <svg class="fill-current flex-1 text-gray-700" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path d="M440.65 12.57l4 82.77A247.16 247.16 0 0 0 255.83 8C134.73 8 33.91 94.92 12.29 209.82A12 12 0 0 0 24.09 224h49.05a12 12 0 0 0 11.67-9.26 175.91 175.91 0 0 1 317-56.94l-101.46-4.86a12 12 0 0 0-12.57 12v47.41a12 12 0 0 0 12 12H500a12 12 0 0 0 12-12V12a12 12 0 0 0-12-12h-47.37a12 12 0 0 0-11.98 12.57zM255.83 432a175.61 175.61 0 0 1-146-77.8l101.8 4.87a12 12 0 0 0 12.57-12v-47.4a12 12 0 0 0-12-12H12a12 12 0 0 0-12 12V500a12 12 0 0 0 12 12h47.35a12 12 0 0 0 12-12.6l-4.15-82.57A247.17 247.17 0 0 0 255.83 504c121.11 0 221.93-86.92 243.55-201.82a12 12 0 0 0-11.8-14.18h-49.05a12 12 0 0 0-11.67 9.26A175.86 175.86 0 0 1 255.83 432z" /></svg>
            </a>
          </div>
          <div class="flex flex-col mr-4 text-center">
            <label for="regular" class="text-xs leading-4 text-gray-700 font-bold uppercase">Color Interval</label> <span class="text-xs font-hairline">( max 100 )</span>
            <input id="regular" v-model="colorInterval" type="number" class="shadow w-full mt-1 border bg-gray-200 border-gray-400 py-1 px-4 text-gray-700 text-md focus:outline-none focus:border-gray-500" placeholder="Input percentage color interval">
          </div>
          <div class="flex flex-col text-center">
            <label for="regular" class="text-xs leading-4 text-gray-700 font-bold uppercase">Color Range</label> <span class="text-xs font-hairline">( 2 - 9 )</span>
            <input id="regular" v-model="colorRange" type="number" class="shadow w-full mt-1 border bg-gray-200 border-gray-400 py-1 px-4 text-gray-700 text-md focus:outline-none focus:border-gray-500" placeholder="Input percentage color interval">
          </div>
        </div>
      </div>
      <hr class="border-gray-400 mx-4 my-4 md:my-0">
      <div class="flex w-full sm:flex-row flex-wrap justify-center">
        <div v-for="(color, index) in colors" :key="index" class="px-4 w-1/2 sm:w-1/3 md:w-1/5 relative">
          <div v-if="color.warning === true" class="text-xs text-red-600 text-right absolute right-0 mr-4 -mt-4">
            Fill 6 Hex Color
          </div>
          <div class="flex mb-4">
            <div class="shadow-md w-8 text-center text-xs py-2 bg-gray-300">
              #
            </div>
            <input
              id="color"
              v-model="color.hex"
              type="text"
              class="shadow-md bg-gray-200 w-full text-sm p-2 outline-none"
              name="color"
              placeholder="HEX COLOR"
              @keyup="updateColor($event, index)"
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
              <p class="text-md py-4 px-4 select-all text-center uppercase hover:opacity-75">
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
      colors: [
        { hex: '6002EE', warning: false },
        { hex: '4CAF50', warning: false },
        { hex: '2196F3', warning: false },
        { hex: 'FFEB3B', warning: false },
        { hex: 'F44336', warning: false }
      ],
      colorRange: 4, // (2 - 9)
      colorInterval: 20, // percentage (max 100)
      interval: 0.20, // percentage (max 1)
      colorShades: []
    }
  },
  watch: {
    colorInterval () {
      if (this.colorInterval > 100) {
        this.colorInterval = 100
      }
      if (this.colorInterval < 0) {
        this.colorInterval = 0
      }
      this.interval = this.colorInterval / 100
      this.colors.forEach((color, index) => {
        this.createTintsAndShades(color.hex, index)
      })
    },
    colorRange () {
      if (this.colorRange > 9) {
        this.colorRange = 9
      }
      if (this.colorRange < 2) {
        this.colorRange = 2
      }
      this.colors.forEach((color, index) => {
        this.createTintsAndShades(color.hex, index)
      })
    }
  },
  created () {
    this.colors.forEach((color, index) => {
      this.createTintsAndShades(color.hex, index)
    })
  },
  methods: {
    updateColor (e, index) {
      const color = e.target.value.replace('#', '')
      if (color.length === 6) {
        this.colors[index].warning = false
        this.createTintsAndShades(color, index)
      } else {
        this.colors[index].warning = true
      }
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
        red: rgb.red * (1 - this.interval * i),
        green: rgb.green * (1 - this.interval * i),
        blue: rgb.blue * (1 - this.interval * i)
      }
    },
    rgbTint (rgb, i) {
      return {
        red: rgb.red + (255 - rgb.red) * i * this.interval,
        green: rgb.green + (255 - rgb.green) * i * this.interval,
        blue: rgb.blue + (255 - rgb.blue) * i * this.interval
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
      const range = this.colorRange
      for (var i = 0; i < range; i++) {
        shadeValues[i] = this.rgbToHex(shadeOrTint(color, i + 1))
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
