<template>
<div class="home">
  <div class="counter">
    <button class="btn" @click="count(-1)"><i class='bx bx-minus'></i></button>
    <p class="number" :class="[{ 'add-active': isAdd }, { 'reduce-active': isReduce }]" :data-before="counter - 1" :data-after="counter + 1">{{counter}}</p>
    <button class="btn" @click="count(1)"><i class='bx bx-plus'></i></button>
  </div>
</div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup () {
    const counter = ref(10)
    const isAdd = ref(false)
    const isReduce = ref(false)
    let allowClick = true
    const count = handler => {
      if (!allowClick) return
      allowClick = false
      handler > 0 ? isAdd.value = true : isReduce.value = true
      setTimeout(() => {
        counter.value += handler
        isAdd.value = false
        isReduce.value = false
        allowClick = true
      }, 200)
    }
    return {
      counter,
      count,
      isAdd,
      isReduce
    }
  }
}
</script>

<style lang="scss" scoped>
.home{
  height: 100vh;
  background-color: #6e6e6e;
  .counter{
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-flow: row nowrap;
    align-self: center;
    justify-content: space-between;
    vertical-align: middle;
    background-color: #000;
    width: 100%;
    max-width: 300px;
    border-radius: 20px;
    overflow: hidden;
    padding: 20px 0;
    overflow: hidden;
    height: 80px;
    &::before{
      content: '';
      width: 100%;
      height: 100%;
      position: absolute;
      background-image: linear-gradient(180deg, #000 0%, #00000080 20%, transparent 50%, #00000080 80%, #000 100%);
      left: 0;
      top: 0;
      z-index: 1;
    }
    .btn, .number{
      display: inline-block;
      vertical-align: middle;
    }
    .number{
      width: 70%;
      font-size: 70px;
      line-height: 80px;
      transform: translateY(-80px);
      &::before{
        display: block;
        content: attr(data-before);
      }
      &::after{
        display: block;
        content: attr(data-after);
      }
    }
    .add-active{
      transform: translateY(-160px);
      transition: transform .2s;
    }
    .reduce-active{
      transform: translateY(0);
      transition: transform .2s;
    }
    .btn{
      width: 20%;
      flex-shrink: 0;
      background-color: #000;
      color: #fff;
      border: none;
      padding: 0;
      font-size: 45px;
      line-height: 2;
      position: relative;
      z-index: 100;
    }
  }
}
</style>