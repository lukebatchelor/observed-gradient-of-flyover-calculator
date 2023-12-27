<template>
  <canvas id="diagramCanvas" ref="canvasEl" width="320" height="200"></canvas>
</template>
<script setup lang="ts">
import rough from "roughjs";
import { onUpdated } from "vue";
import { onMounted, ref, defineProps } from "vue";

const props = defineProps<{ a1Negative: boolean }>();

type Point = { x: number; y: number };

const canvasEl = ref();
let roughCanvas: ReturnType<typeof rough.canvas>;

onMounted(() => {
  roughCanvas = rough.canvas(canvasEl.value, { options: { stroke: "white" } });
  if (!props.a1Negative) {
    drawDiagram1();
  } else {
    drawDiagram2();
  }
});
onUpdated(() => {
  if (!props.a1Negative) {
    console.log("redraw");
    drawDiagram1();
  } else {
    drawDiagram2();
    console.log("dont draw");
  }
});

const drawDiagram1 = () => {
  const ctx = canvasEl.value.getContext("2d") as CanvasRenderingContext2D;
  ctx.strokeStyle = "white";
  ctx.fillStyle = "white";
  const ptA: Point = { x: 320, y: 100 };
  const ptB: Point = { x: 150, y: 150 };
  const ptC: Point = { x: 10, y: 20 };

  // triangle
  roughCanvas.line(ptA.x, ptA.y, ptB.x, ptB.y);
  roughCanvas.line(ptB.x, ptB.y, ptC.x, ptC.y);
  roughCanvas.line(ptC.x, ptC.y, ptA.x, ptA.y);

  // horizon lines
  const horizonLineLength = 120;
  const ptAHorizon = { x: ptA.x - horizonLineLength, y: ptA.y };
  const ptBHorizon = { x: ptB.x - horizonLineLength, y: ptB.y };
  const ptCHorizon = { x: ptC.x + horizonLineLength, y: ptC.y };
  dashedLine(ptA, ptAHorizon);
  dashedLine(ptB, ptBHorizon);
  dashedLine(ptC, ptCHorizon);

  drawAngleBetweenPts("A1", ptC, ptA, ptAHorizon, { arcDist: 80 }); // angle a1
  drawAngleBetweenPts("A2", ptAHorizon, ptA, ptB, { arcDist: 60 }); // angle a2
  drawAngleBetweenPts("B", ptC, ptB, ptA); // angle b
  drawAngleBetweenPts("X", ptBHorizon, ptB, ptC, { arcDist: 40 }); // angle b to horiz
  drawAngleBetweenPts("C", ptB, ptC, ptA, { arcDist: 50 }); // angle c
  drawAngleBetweenPts("Y", ptCHorizon, ptC, ptA, { arcDist: 70 }); // angle y
  drawAngleBetweenPts("G", ptCHorizon, ptC, ptB, { arcDist: 100 }); // angle G

  // label sides
  const labelA = {
    x: (ptA.x - ptB.x) / 2 - 5,
    y: ptB.y + (ptA.y - ptB.y) / 2 - 20,
  };
  const labelB = {
    x: (ptA.x - ptC.x) / 2,
    y: ptC.y + (ptA.y - ptC.y) / 2 - 10,
  };
  const labelC = {
    x: ptB.x + (ptA.x - ptB.x) / 2,
    y: ptB.y + (ptA.y - ptB.y) / 2 + 10,
  };
  ctx.fillText("a", labelA.x, labelA.y);
  ctx.fillText("b", labelB.x, labelB.y);
  ctx.fillText("c", labelC.x, labelC.y);
};

const drawDiagram2 = () => {
  const ctx = canvasEl.value.getContext("2d") as CanvasRenderingContext2D;
  ctx.clearRect(0, 0, canvasEl.value.width, canvasEl.value.height);
  ctx.strokeStyle = "white";
  ctx.fillStyle = "white";
  const ptA: Point = { x: 320, y: 50 };
  const ptB: Point = { x: 150, y: 150 };
  const ptC: Point = { x: 10, y: 100 };

  // triangle
  roughCanvas.line(ptA.x, ptA.y, ptB.x, ptB.y);
  roughCanvas.line(ptB.x, ptB.y, ptC.x, ptC.y);
  roughCanvas.line(ptC.x, ptC.y, ptA.x, ptA.y);

  // horizon lines
  const horizonLineLength = 120;
  const ptAHorizon = { x: ptA.x - horizonLineLength, y: ptA.y };
  const ptBHorizon = { x: ptB.x - horizonLineLength, y: ptB.y };
  const ptBHorizon2 = { x: ptB.x + horizonLineLength, y: ptB.y };
  dashedLine(ptA, ptAHorizon);
  dashedLine(ptB, ptBHorizon);
  dashedLine(ptB, ptBHorizon2);

  drawAngleBetweenPts("A1", ptC, ptA, ptAHorizon, { arcDist: 80 }); // angle a1
  drawAngleBetweenPts("A2", ptAHorizon, ptA, ptB, { arcDist: 60 }); // angle a2
  drawAngleBetweenPts("B", ptC, ptB, ptA); // angle b
  drawAngleBetweenPts("X", ptBHorizon, ptB, ptC, { arcDist: 40 }); // angle b to horiz
  drawAngleBetweenPts("C", ptB, ptC, ptA, { arcDist: 50 }); // angle c
  drawAngleBetweenPts("Y", ptA, ptB, ptBHorizon2, { arcDist: 40 }); // angle y

  // label sides
  const labelA = {
    x: ptC.x + (ptB.x - ptC.x) / 2 - 5,
    y: ptC.y + (ptB.y - ptC.y) / 2 + 10,
  };
  const labelB = {
    x: (ptA.x - ptC.x) / 2,
    y: ptC.y + (ptA.y - ptC.y) / 2 - 10,
  };
  const labelC = {
    x: ptB.x + (ptA.x - ptB.x) / 2,
    y: ptB.y + (ptA.y - ptB.y) / 2 + 10,
  };
  ctx.fillText("a", labelA.x, labelA.y);
  ctx.fillText("b", labelB.x, labelB.y);
  ctx.fillText("c", labelC.x, labelC.y);
};

function dashedLine(pt1: Point, pt2: Point) {
  roughCanvas.line(pt1.x, pt1.y, pt2.x, pt2.y, {
    strokeLineDash: [10, 5],
  });
}

type AngleOpts = {
  arcDist?: number;
};
function drawAngleBetweenPts(
  label: string,
  pt1: Point,
  pt2: Point,
  pt3: Point,
  opts: AngleOpts = {}
) {
  const ctx = canvasEl.value.getContext("2d") as CanvasRenderingContext2D;
  const arcDist = opts.arcDist || 20;
  let dirA = direction(pt2, pt1);
  let dirB = direction(pt3, pt2);
  dirB += Math.PI;
  let sweepAngle = dirB - dirA;
  let startAngle = dirA;
  if (Math.abs(sweepAngle) > Math.PI) {
    sweepAngle = Math.PI * 2 - sweepAngle;
    startAngle = dirB;
  }
  ctx.beginPath();
  if (sweepAngle < 0) {
    // if the angle is sweeping anticlockwise
    ctx.arc(pt2.x, pt2.y, arcDist, startAngle + sweepAngle, startAngle);
  } else {
    // draw clockwise angle
    ctx.arc(pt2.x, pt2.y, arcDist, startAngle, startAngle + sweepAngle);
  }
  ctx.stroke(); // all done
  const textX = pt2.x + Math.cos(startAngle + sweepAngle / 2) * (arcDist + 15);
  const textY = pt2.y + Math.sin(startAngle + sweepAngle / 2) * (arcDist + 15);
  ctx.fillText(label, textX, textY);
}

const direction = (pt1: Point, pt2: Point) => {
  let angleBetween = Math.acos(
    (pt2.x - pt1.x) / Math.sqrt((pt1.x - pt2.x) ** 2 + (pt1.y - pt2.y) ** 2)
  );
  if (pt1.y > pt2.y) angleBetween = -angleBetween;
  return angleBetween;
};
</script>
