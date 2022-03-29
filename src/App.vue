<template>

  <div class="graph-section">

    <div class="graph">
      <h4 class="graph__title">Приток / Отток - за последние 30 дней</h4>
      <div class="graph__wrapper">

        <transition-group name="graphAm">
          <div class="graph-container" v-if="isSync">
            <div class="axis-wrapper">
              <p class="axis-top">10</p>
              <p class="axis-bottom">0</p>
            </div>

            <ul class="graph__main">
              <li class="graph__item" v-for="index in 30" :key="index">
          <span
              :class="['item__background',
              {'line--active': currentLine === index}]"
              :style="'top: ' + ((i - 1) * 8) + 'px;'"
              v-for="i in 22"
              :key="i"
          ></span>
                <graph-lines :index="index" @lineActive="lineActive($event, index)" />
              </li>
            </ul>

            <div class="graph__bottom">

              <div class="graph__info">
                <div class="info__item">
                  <span class="info__color item--yellow"></span>
                  <p class="info__text">Приток</p>
                </div>
                <div class="info__item">
                  <span class="info__color item--grey"></span>
                  <p class="info__text">Отток</p>
                </div>
              </div>

              <a class="graph__about">Подробнее</a>

            </div>
          </div>

          <p class="need-sync" v-else>
            Необходимо выполнить синхронизацию с вашей crm системой
          </p>
        </transition-group>

      </div>

    </div>

    <div class="graph">
        <h4 class="graph__title">Жизненный цикл клиентов</h4>
        <div class="graph__wrapper">

          <transition-group name="graphAm">

            <graph-circle v-if="isSync" key="1" />

            <div class="preloader-wrapper" v-else key="2">
              <preloader />
            </div>

          </transition-group>

        </div>

    </div>

  </div>
</template>

<script>
import {ref} from "vue";
import graphLines from "@/components/graph-lines";
import preloader from "@/components/preloader";
import graphCircle from "@/components/graph-circle";

export default {
  name: 'App',
  components: {
    graphLines,
    preloader,
    graphCircle
  },
  setup() {

    const isSync = ref(false);

    setTimeout(() => {
      isSync.value = true;
    }, 7000)

    const currentLine = ref(0);

    function lineActive(state, index) {
      if(state) {
        currentLine.value = index;
      } else {
        currentLine.value = 0;
      }

    }

    return { lineActive, currentLine, isSync }

  }
}
</script>

<style src="./assets/css/main.css"></style>
