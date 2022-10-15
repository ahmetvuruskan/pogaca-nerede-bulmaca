<template>
<transition-group name="slideContainer" mode="out-in">
  <component key="mainComponent"
      @isCorrectEvent="activeComponent=$event"
      :is="activeComponent" >
  </component>
  <canvas v-show="activeComponent == 'celebrate'" key="canvas" id="canvas" ></canvas>
</transition-group>
</template>
<script>
import GameCards from "./components/GameCards";
import Failure from "./components/Failure";
import Celebrate from "./components/Celebrate"

export default {
  data : ()=>{
    return {
      activeComponent   : "gameCards"
    }
  },
  components:{
    gameCards : GameCards,
    failure : Failure,
    celebrate : Celebrate
  },

}
</script>
<style>
.slideContainer-enter{}
.slideContainer-enter-active{
  animation: slide-in 0.3s ease-in-out forwards ;

}
.slideContainer-leave{}
.slideContainer-leave-active{
  animation: slide-out 0.3s ease-in-out forwards ;
}

@keyframes slide-in {
  from{
    transform: translateX(-1000px);
    opacity: 0;
}
  to{
   transform: translateX(0px);
    opacity:1 ;
  }
}
@keyframes slide-out {
  from{
    transform: translateX(0px);
    opacity: 1;
  }
  to{
    transform: translateX(1000px);
    opacity: 0;
  }
}
body{
  font-family: sans-serif;
}
</style>
