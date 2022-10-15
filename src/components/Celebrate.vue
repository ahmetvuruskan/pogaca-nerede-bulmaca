<template>
  <div class="container">
    <h1>Tebrikler Bildiniz!!!!!</h1>
    <button @click="newGame" >Yeni Oyun</button>
  </div>
</template>

<script>
export default {
  methods :{
    newGame(){
      this.$emit("isCorrectEvent","gameCards");
    }
  }
}

</script>

<style scoped>
.container{
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: white;
}
.container h1{
  text-align: center;
  font-size: 333%;
  opacity: 0.5;
  color: darkgreen;
}
.container button{
  width: 200px;
  background-color: #fff;
  color: darkred;
  border: 1px solid darkgreen;
  height: 50px;
  font-size: 15px;
  border-radius: 5px;
  outline: none;
  transition: all 0.5s;
  cursor: pointer;
}
.container button:hover{
  background-color: darkgreen;
  color: #fff;
  transition: all 0.5s;
}
</style>