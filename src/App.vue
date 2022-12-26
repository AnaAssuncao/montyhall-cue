<template>
  <div class="doors">
    <div v-for="door in amountDoor" :key="door" @click="handleSelectDoor(door)">
     <Door 
        :isSelect='door == select' 
        :hasGift='chosenDoor == door' 
        :isOpen='isOpen.includes(door)' 
        :doorNumber="door"></Door>
    </div>
  </div>

  <div v-if='isOpen.length<3'>
      <button class='door-btn' @click="handleOpenDoor()">Abrir uma porta</button>
    </div>
    <div v-if='isOpen.length===3'>
      <button class='door-btn' @click="handleResponse()">Porta com presente</button>
    </div>
    <div>
      <button class='door-btn' @click="handleRestart()">Reiniciar</button>
    </div>
    <div>
      <p>{{ msgDoor }}</p>
    </div>
</template>

<script>
import Door from "./components/Door"

const chosenDoor = Math.floor(Math.random() * 5 + 1)
export default {
  name: 'App',
  components: {
    Door
  },
  data(){
    return{
      amountDoor:5,
      chosenDoor: chosenDoor,
      select: 0,
      isOpen:[],
      msgDoor:''
    }
  },
  methods: {
    handleSelectDoor(number){
      this.select=number
    },
    handleOpenDoor(){
      if(this.select===0){
        alert("Selecione uma porta");
        return
      }

      const number = Math.floor(Math.random() * 5 + 1)
      if(number!==this.chosenDoor && this.select!==number && !this.isOpen.includes(number)){
        this.isOpen.push(number)
        this.msgDoor = 'Quer mudar a porta selecionada?'
        return
      }

      this.handleOpenDoor()
    },
    handleResponse(){
        this.isOpen.push(this.chosenDoor)
        this.msgDoor = this.select === this.chosenDoor ? "Parabéns, você acertou!": "Não foi dessa vez, tente novamente!"
    },
    handleRestart(){
      this.isOpen=[]
      this.select=0
      this.msgDoor=''
      const chosenDoor = Math.floor(Math.random() * 5 + 1)
      this.chosenDoor=chosenDoor
    },
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.doors{
  display: flex;
  justify-content: center;
  align-content: center;
}
.door-btn{
  background-color: crimson;
  border-radius:20px;
  cursor: pointer;
  font-size: 14px;
  margin:24px;
  padding:16px;
}

</style>
