<template>
  <div class="graph-circle__main">

    <div class="wrapper">
      <p class="center__text">Все клиенты по сегментам</p>

      <diagram-component />
    </div>

    <ul class="graph__stat">
      <li class="stat__item">
        <span class="stat__color yellow"></span>
        <p class="stat__percent">41%</p>
        <p class="stat__text">Новички</p>
      </li>
      <li class="stat__item">
        <span class="stat__color green"></span>
        <p class="stat__percent">39%</p>
        <p class="stat__text">Активные</p>
      </li>
      <li class="stat__item">
        <span class="stat__color grey"></span>
        <p class="stat__percent">13%</p>
        <p class="stat__text">Отток</p>
      </li>
      <li class="stat__item">
        <span class="stat__color grey--dark"></span>
        <p class="stat__percent">7%</p>
        <p class="stat__text">Потерянные</p>
      </li>
    </ul>

  </div>
</template>

<script>
import {ref, computed} from "vue";
import diagramComponent from "@/components/diagram-component";

export default {
  name: "graph-circle",
  components: {
    diagramComponent
  },
  setup() {

    const wrapper = ref(null);

    const wrapperParams = computed(() => {

      if(wrapper.value) {
        const width = wrapper.value.clientWidth;
        const height = wrapper.value.clientHeight;

        return { width, height }
      }
      return 0;

    })


    return { wrapper, wrapperParams }

  }
}
</script>

<style scoped>

.wrapper {
  position: relative;
  width: 260px;
  height: 260px;
}

.graph-circle__main {
  display: flex;
}

.graph__circle {
  position: relative;

  width: 260px;
  height: 260px;
  margin-right: 75px;

  overflow: hidden;
}

.graph__circle::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;

  width: 250px;
  height: 250px;

  border-radius: 50%;
  border: 60px solid #fff;
  transform: translateX(-50%) translateY(-50%);
}

.circle__color {
  position: absolute;
}

.circle__color1 {
  top: -5px;
  left: -5px;

  width: 50%;
  height: 75%;
}

.circle__color2 {
  top: -5px;
  right: -5px;

  width: 50%;
  height: 30%;
}

.circle__color3 {
  bottom: -5px;
  right: -5px;

  width: 30%;
  height: 70%;
}

.circle__color4 {
  bottom: -5px;
  left: -5px;

  width: 70%;
  height: 25%;
}

.circle__center {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 5;

  display: flex;
  justify-content: center;
  align-items: center;

  width: 230px;
  height: 230px;

  border-radius: 50%;
  transform: translateX(-50%) translateY(-50%);

  background-color: #fff;;
}

.center__text {
  position: absolute;
  top: 115px;
  left: 21px;

  max-width: 220px;

  font-size: 18px;
  line-height: 26px;
  text-align: center;
}

.graph__stat {
  display: flex;
  flex-direction: column;
  justify-content: center;

  margin-left: 70px;
}

.stat__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 180px;
  margin: 15px 0;

  font-size: 16px;
}

.stat__text {
  width: 85px;
}

.stat__color {
  display: block;
  width: 24px;
  height: 24px;
  margin-right: 25px;

  border-radius: 7px;
}

.stat__percent {
  margin-right: 20px;
  font-weight: 500;
}

.green {
  background-color: #4ADDBC;
}

.grey--dark {
  background-color: #575C62;
}
</style>