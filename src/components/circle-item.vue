<template>
    <span ref="circle" :style="stylePosition">
      <span :class="['border', 'top']" :style="borderStyle1"></span>
      <span :class="['border', 'bottom']" :style="borderStyle2"></span>
    </span>
</template>

<script>
import {ref, computed} from "vue";

export default {
  name: "circle-item",
  props: {
    wrapperParams: {
      type: Object,
      required: true
    },
    left: {
      type: String,
      required: false
    }
  },
  setup(props) {

    const circle = ref(null);
    const xCoords = ref(0);
    const yCoords = ref(0);

    const radius = computed(() => {
      if(circle.value) {
        return props.wrapperParams.width / 2;
      }
      return 0;
    })

    function calcCoords(pos) {
      let coords

      if(pos === 'top') {
        // coords = circle.value.clientWidth;
        yCoords.value = Math.sqrt(Math.abs(Math.pow(coords, 2) - (Math.pow(Number(radius.value), 2))));
      } else {
        // coords = circclientHeightle.value.;
        xCoords.value = radius.value - Math.sqrt(Math.abs((Math.pow(Number(radius.value), 2) - Math.pow(coords, 2))));
      }

    }
    setTimeout(() => {
      calcCoords('bottom');
      calcCoords('top');

      // console.log(circle.value.getBoundingClientRect())
    }, 500)

    const blockCoords = computed(() => {

      if(circle.value && !props.left) {
        return {
          start: (radius.value * 2) - circle.value.clientWidth + 12,
          end: radius.value * 2
        };
      } else if(circle.value && props.left) {
        return {
          start: 0,
          end: circle.value.clientWidth + 12
        }
      }
      return 0;

    })

    // const styleX = computed(() => {
    //   if(!props.left && circle.value) {
    //     return 'left: ' + positionX.value + 'px;'
    //   }
    //   return 'left: 0px;'
    // })

    const stylePosition = computed(() => {

      let style = '';

      if(circle.value) {

        if(!props.left) {
          style += 'left: ' + blockCoords.value.start + 'px; '
        } else {
          style = '';
        }

        // const currentX = blockCoords.value.start - radius.value;
        // const a = Math.sqrt(radius.value * radius.value - currentX * currentX)
        //
        // style += 'top: ' + (radius.value - a) + 'px;';

        return style

      }
      return 0
    })

    const borderStyle1 = computed(() => {

      console.log(Number(radius.value), Number(blockCoords.value.start - radius.value))
      const a = Math.sqrt(Math.pow(Number(radius.value), 2) - Math.pow(Number(blockCoords.value.start - radius.value), 2));

      return 'top: ' + a + 'px;';

    })

    const borderStyle2 = computed(() => {

      const a = Math.sqrt(Math.pow(Number(radius.value), 2) - Math.pow(Number(blockCoords.value.end - radius.value), 2))

      return 'top: ' + a + 'px;';

    })


    return { circle, stylePosition, borderStyle1, borderStyle2 }

  }
}
</script>

<style scoped>

.border {
  position: absolute;

  width: 12px;
  height: 12px;
  border-radius: 50%;

  background-color: inherit;
}

.right {
  left: calc(100% - 6px);
}

.left {

}

.bottom {
  bottom: -6px;
}

</style>