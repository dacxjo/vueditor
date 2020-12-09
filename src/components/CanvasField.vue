<template>
  <div ref="canvasWrapper"></div>
</template>

<script>
import { onMounted, ref } from "vue";
export default {
  setup() {
    const canvasWrapper = ref(null);
    const stage = ref(null);

    function responsiveCanvas() {
      const stageWidth = canvasWrapper.value.offsetWidth;
      const stageHeight = canvasWrapper.value.offsetHeight;
      const containerWidth = canvasWrapper.value.offsetWidth;
      const containerHeight = canvasWrapper.value.offsetHeight;

      var scale = containerWidth / stageWidth;

      stage.value.width(stageWidth * scale);
      stage.value.height(stageHeight * scale);
      stage.value.scale({ x: scale, y: scale });
      stage.value.draw();
    }

    function setupCanvas() {
      const width = canvasWrapper.value.offsetWidth;
      const height = canvasWrapper.value.offsetHeight;

      stage.value = new Konva.Stage({
        container: canvasWrapper.value,
        width: width,
        height: height,
      });

      var layer = new Konva.Layer();

      var circle = new Konva.Circle({
        x: stage.value.width() / 2,
        y: stage.value.height() / 2,
        radius: 70,
        fill: "red",
        stroke: "black",
        strokeWidth: 4,
        draggable: true,
      });

      layer.add(circle);

      const tr = new Konva.Transformer();

      layer.add(tr);

      tr.nodes([circle]);

      stage.value.add(layer);

      layer.draw();
    }

    onMounted(() => {
      setupCanvas();

      responsiveCanvas();

      window.addEventListener("resize", responsiveCanvas);
    });

    return {
      canvasWrapper,
      stage,
    };
  },
};
</script>