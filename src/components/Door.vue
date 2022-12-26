<template>
  <div class="door-area">
    <div class="door-frame" :class="{selected : !isOpen && isSelect}">
      <div class="door-gift" >
        <Gift v-if="hasGift" />
      </div>
    </div>
    <div class="door" v-show="!isOpen" >
      <div class="door-number" :class="{'selected-number' : isSelect}">{{doorNumber}}</div>
      <div class="door-handle"  :class="{selected : isSelect}"></div>
    </div>
  </div>
</template>

<script>
import Gift from './Gift'

export default {
  name: 'Door-montyhall',
  components: {
    Gift
  },
  props:{
    isSelect:  Boolean,
    hasGift:  Boolean,
    isOpen:  Boolean,
    doorNumber: Number,
  }
}
</script>

<style>
:root {
  --door-border: 5px solid brown;
  --selected-border: 5px solid yellow;
}

.door-area {
  position: relative;
  cursor:pointer;
  width: 200px;
  height: 310px;
  border-bottom: 10px solid #AAA;
  margin-bottom: 20px;
  font-size: 3rem;
  margin: 32px;

  display: flex;
  justify-content: center;
}

.door-frame {
    position: absolute;
    height: 100%;
    width: 100%;

    border-left: var(--door-border);
    border-top: var(--door-border);
    border-right: var(--door-border);

    display: flex;
    justify-content: center;
    align-items: flex-end;
}

.door {
  position: absolute;
  top: 5px;
  height: 280px;
  width: 170px;
  background-color: chocolate;

  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px;
  z-index: 2;
}

.door-frame.selected {
  border-left: var(--selected-border);
  border-top: var(--selected-border);
  border-right: var(--selected-border);
}
.door-number{
  color:white;
}

.door-handle{
  height: 20px;
  width: 20px;
  border-radius: 10px;
  background-color: rgb(165, 42, 42);
  margin-top: 100px;
  margin-right: 150px;
}

.selected {
  background-color: yellow;
}
.selected-number {
  color: yellow;
}

</style>
