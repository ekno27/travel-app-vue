
<template>
<div>
     <div class="jumbotron">
        <h1>Hello{{name}}</h1>
        <div class="form-group">
                <h4>{{prompt}}</h4>
                <div v-show="hide === false">
                  <input type="text" class="form-control" id="input-form" :placeholder="placeholder" v-model="currentName">
                  <button type="button" class="btn btn-primary" id="submit" @click="submit">Submit</button>
                </div>
            </div>
    </div><!--End of jumbotron-->
    <!-- <sideComponent/> -->
    <div class="container">
        <div class="row">
            <div class="col-md-4" id="cities">
                <h2 v-show="hide === true" id="city-prompt">Click on a button to get more info</h2>
                <div id="city-buttons">
                  <button @click="info(city)" class="btn" v-for="city in cities" :key="city">
                  {{city}}
                  </button>
                </div>
            </div>
            <div class="col-md-2"></div>
            <div class="col-md-6" id="city-info">
              <div v-show="hide === true">
                <h2 id="current-city">{{currentCity}}</h2>
                <p id="city-details">{{currentCity}} has {{letterCount}}
                letters in it. The first letter is{{currentCity.charAt(0)}}.
                The last letter is {{currentCity.charAt(currentCity.length-1)}}.
                The first three letters are {{firstThree}},
                the last three are {{lastThree}}. Spelled backwards, it's {{backwards}}</p>
              </div>
            </div>
        </div>
    </div>
</div>
</template>
<script>
// import sideComponent from '@/components/sideComponent'
export default {
  name: 'MainComponent',
  data () {
    return {
      letterCount: 0,
      lastLetter: '',
      firstThree: '',
      lastThree: '',
      backwards: '',
      hide: false,
      placeholder: 'Example: Eric',
      prompt: 'What is your name?',
      emptyName: true,
      emptyList: true,
      name: '',
      // currentCities: '',
      cities: [],
      msg: 'This is the main component',
      currentName: '',
      currentCity: ''
    }
  },
  methods: {
    submit () {
      if (this.emptyName === true) {
        this.placeholder = 'Example: London, Japan, New Dorp'
        this.prompt = 'What places have you traveled to?'
        this.emptyName = false
        this.name = ', ' + this.currentName
        this.currentName = ''
      } else if (this.emptyList === true) {
        this.cityProcessing()
        // console.log('hello')
        this.currentCities = this.currentName
        this.hide = true
      }
    },
    cityProcessing () {
      this.cities = this.currentName.split(', ')
      console.log(this.cities)
      if (this.cities.length < 3) {
        this.prompt = `You need to travel more${this.name}`
      } else {
        this.prompt = 'Wow, well traveled!'
      }
    },
    info (city) {
      this.lastLetter = ''
      this.firstThree = ''
      this.lastThree = ''
      this.backwards = ''
      this.currentCity = city
      this.letterCount = city.length
      console.log(city)
      for (var i = 0; i < city.length; i++) {
        if (i < 3) {
          this.firstThree += city.charAt(i)
        }
        if (i > city.length - 4) {
          this.lastThree += city.charAt(i)
        }
        this.backwards = city.charAt(i) + this.backwards
      }
    }
  }
//   components: {sideComponent}
}
</script>

<style>
h1,
h4,
button {
    text-align: center;
}

</style>
