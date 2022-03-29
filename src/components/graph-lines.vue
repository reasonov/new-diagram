<template>
  <div
      class="wrapper"
      :style="maxHeight"
      @mouseenter="getInfo(true)"
      @mouseleave="getInfo(false)"
  >
    <span
        class="graph__line yellow"
        :style="'height: ' + itemParams.plus + 'px;'"
    ></span>
    <span
        class="graph__line graph__line--grey"
        :style="'height: ' + itemParams.minus + 'px;'"
    ></span>
    <div class="graph__popup" v-show="infoVisible">
      <p class="popup__month">Январь {{ index }}</p>
      <p class="popup__block">
        <span class="popup__color grey"></span>
        <span class="popup__text">Отток 24</span>
      </p>
      <p class="popup__block">
        <span class="popup__color yellow"></span>
        <span class="popup__text">Приток 36</span>
      </p>
    </div>
  </div>
</template>

<script>
import {ref, reactive, computed} from "vue";

export default {
  name: "graph-item",
  props: {
    index: {
      type: Number,
      required: true
    }
  },
  setup(props, { emit }) {

    function getRandom(min, max) {
      return Math.random() * (max - min) + min;
    }

    const itemParams = reactive({
      plus: 0,
      minus: 0
    })

    itemParams.plus = getRandom(0, 180);
    itemParams.minus = getRandom(0, 180);

    const maxHeight = computed(() => {
      return 'min-height: ' + Math.max(itemParams.plus, itemParams.minus) + 'px;';
    })

    const infoVisible = ref(false);

    function getInfo(state) {
      infoVisible.value = state;

      emit('lineActive', state);
    }

    return {
      itemParams,
      infoVisible,
      getInfo,
      maxHeight
    }

  }
}
</script>

<style scoped>

.wrapper {
  position: relative;
}

.graph__popup {
  position: absolute;
  top: 0;
  left: 10px;
  z-index: 5;
  
  width: 123px;
  height: 92px;
  padding: 10px;

  border-radius: 10px;
  box-sizing: border-box;

  font-size: 15px;
  line-height: 26px;
  color: #fff;

  background-color: #575C62;
}

.popup__block {
  display: flex;
  align-items: center;
}

.popup__color {
  display: block;
  width: 8px;
  height: 8px;
  margin-right: 5px;
  border-radius: 50%;
}
</style>