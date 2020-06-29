<template>
  <div>
    <h1>
      {{msg}}
    </h1>
    <div class="mdl-card mdl-shadow--2dp">
      <div class="mdl-card__title">
        <h2 class="mdl-card__title-text">{{cacheQuestion.Q}}</h2>
      </div>
      <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label is-dirty" v-if="!cacheQuestion.isKnown">
        <div>
          <textarea type="text" rows="4" class="mdl-textfield__input"></textarea>
          <label class="mdl-textfield__label">try it</label>
        </div>
      </div>
      
      <div class="mdl-card__supporting-text" v-show="cacheQuestion.isShowAnswer">{{cacheQuestion.A}}</div>
      <button class="mdl-button mdl-js-button mdl-button--raised mdl-js-ripple-effect mdl-button--accent" v-if="!cacheQuestion.isShowAnswer" @click="showAnswer">
        show answer
      </button>
      <!-- <button class="mdl-button mdl-js-button mdl-button--raised mdl-js-ripple-effect mdl-button--colored" v-if="cacheQuestion.isShowAnswer" @click="known">
        I know this!
      </button> -->
    </div>
    <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" @click="next">
      next
    </button>
  </div>
</template>

<script>
import json from '../../static/data.json'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Vue test',
      data:json.data,
      random:2,
      cacheQuestion:{
        Q:'',
        A:'',
        isKnown:false,
        isShowinput:true,
        isShowAnswer:false
      },
      max:9,
      min:0
    }
  },
  created(){
    const vm = this
    vm.random = Math.floor(Math.random() * (vm.max - vm.min) + vm.min)
    vm.cacheQuestion.Q = vm.data[vm.random].Q
    vm.cacheQuestion.A = vm.data[vm.random].A
    vm.cacheQuestion.isKnown = vm.data[vm.random].isKnown
    vm.cacheQuestion.isShowAnswer = vm.data[vm.random].isKnown
    vm.cacheQuestion.isShowinput = !vm.data[vm.random].isKnown
},
  methods:{
    showAnswer(){
      const vm = this
      vm.cacheQuestion.isShowAnswer = true
    },
    next(){
      const vm =this
      vm.random = Math.floor(Math.random() * (vm.max - vm.min) + vm.min);
      console.log(vm.random)
      vm.cacheQuestion.Q = vm.data[vm.random].Q
      vm.cacheQuestion.A = vm.data[vm.random].A
      vm.cacheQuestion.isKnown = vm.data[vm.random].isKnown
      vm.cacheQuestion.isShowAnswer = vm.data[vm.random].isKnown
      vm.cacheQuestion.isShowinput = !vm.data[vm.random].isKnown
    },
    known(){
      console.log('k')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mdl-card{
  margin: 0 auto 2rem auto;
}
.mdl-card__supporting-text{
  text-align: left;
}
.mdl-textfield{
  margin: auto;
}
</style>
