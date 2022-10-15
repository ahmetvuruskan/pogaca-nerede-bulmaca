<template>
  <div class="game-area">
<p>{{answer}}</p>
    <h1 class="title">Poğaça <span>Nerede</span> <strong> ?</strong></h1>
    <h4 class="description">Açık kartlardan birini seçtikten sonra, kapalı karta tıklayınız.</h4>
    <div class="container">
   <transition-group name="rotate-all" appear class="container" >
     <card :key="card.id" :class="{'shadow':selectedCard === card.id}" @click.native="selectedCard = card.id" v-for="card in cards"
           :card="card"></card>
   </transition-group>
    </div>
    <div class="container">
<transition name="rotate" mode="out-in">
  <component @click.native="showCard(answer)" :is="activeCard" :card="answer"  ></component>
</transition>
    </div>
  </div>
</template>

<script>
import Card from "./Card";
import DefaultCard from "./DefaultCard"

export default {
  components: {
    card: Card,
    defaultCard: DefaultCard
  },
  data: () => {
    return {
      cards: [
        {id: 1, component: "card", image: "/src/assets/card-1.jpg"},
        {id: 2, component: "card", image: "/src/assets/card-2.jpg"},
        {id: 3, component: "card", image: "/src/assets/card-3.jpg"},
        {id: 4, component: "card", image: "/src/assets/card-4.jpg"},
        {id: 5, component: "card", image: "/src/assets/card-5.jpg"},
      ],
      selectedCard: null,
      answer: {},
      activeCard : "defaultCard"
    }
  },
  created() {
    let answer = Math.ceil(Math.random() * this.cards.length);
    this.answer = this.cards[answer - 1];
  },
  methods:{
    showCard(answer){
      console.log(this.selectedCard)
      if (this.selectedCard==null){
        alert("Lütfen yukarıdan bir kart seçiniz");
      }else{
        this.activeCard = answer.component;
        setTimeout(()=>{
          if (answer.id == this.selectedCard){
            this.$emit("isCorrectEvent","celebrate");
          }else{
            this.$emit("isCorrectEvent","failure");
          }
        },2500)
      }


    }
  }
}
</script>

<style scoped>
.title {
  text-align: center;
  color: rosybrown;
}
.title span {
  color: mediumpurple;
}
.title strong {
  color: darkred;
}
.description {
  color: grey;
  text-align: center;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 50px;

}
.shadow {
  box-shadow: 0px 5px 48px #30969f !important;
  transition: box-shadow .5s;
}
/*** Açık kartların animasyonları için transition classları ***********/

.rotate-all-enter{}
.rotate-all-enter-active{
animation: rotate-all ease-in-out 2s forwards;
}
.rotate-all-leave{}
.rotate-all-leave-active{}

@keyframes rotate-all {
  from{
    transform:  rotateY(0);
  }
  to{
    transform: rotateY(720deg);
  }
}
/* Kapalı kartın anımasyonu için transition classları **/
.rotate-enter{}
.rotate-enter-active{
  animation: rotate-in 1s ease-in-out forwards;
}
.rotate-leave{}

.rotate-leave-active{
  animation: rotate-out 1s ease-in-out forwards;
}

@keyframes rotate-in {
  from {
    transform: rotateY(90deg);
  }
  to{
    transform: rotateY(0deg);
  }
}
@keyframes rotate-out {
  from {
    transform: rotateY(0deg);
  }
  to{
    transform: rotateY(90deg);
  }
}
</style>