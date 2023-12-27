<template>
  <v-container class="fill-height">
    <v-responsive class="text-center fill-height">
      <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>

      <h1 class="text-h3 font-weight-bold handwriting">
        Brett's
        <span style="whitespace: nowrap; display: block"
          ><s class="straight" :style="{ fontSize: '0.5em' }"
            >Observed Gradient</s
          ><s :style="{ fontSize: '0.3em' }">of</s
          ><s :style="{ fontSize: '0.1em' }">Fly Over</s></span
        >
        <s :style="{ fontSize: '0.7em' }">Angel's</s>
        Angles
      </h1>

      <div class="py-8"></div>

      <v-form v-model="valid">
        <v-container>
          <v-row>
            <v-col cols="6">
              <v-text-field
                v-model="angleA1"
                @change="angleA1 = Number(angleA1)"
                label="Angle A₁"
                type="number"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field
                v-model="angleA2"
                @change="angleA2 = Number(angleA2)"
                label="Angle A₂"
                type="number"
                required
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="6">
              <v-text-field
                v-model="sideB"
                @change="sideB = Number(sideB)"
                label="Side b"
                type="number"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field
                v-model="sideC"
                @change="sideC = Number(sideC)"
                label="Side c"
                type="number"
                required
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
      <div class="text-body-2 font-weight-light mb-n1">
        <v-container>
          <v-row>
            <v-col> Side a = {{ sideA.toFixed(2) }}m </v-col>
          </v-row>
          <v-row>
            <v-col> Angle B = {{ angleB.toFixed(2) }}deg </v-col>
          </v-row>
          <v-row>
            <v-col> Angle C = {{ angleC.toFixed(2) }}deg </v-col>
          </v-row>
          <v-row>
            <v-col>
              Observed Gradient = {{ observedGradientPct.toFixed(2) }}%
            </v-col>
          </v-row>
        </v-container>
        <v-expansion-panels>
          <v-expansion-panel title="Calculations">
            <v-expansion-panel-text class="text-left">
              <Diagram :a1-negative="angleA1 < 0" />
              <MathCalcs
                :angle-a1="angleA1"
                :angle-a2="angleA2"
                :side-a="sideA"
                :side-b="sideB"
                :side-c="sideC"
                :angle-a-rad="angleARad"
                :angle-b="angleB"
                :angle-c="angleC"
                :angle-g="angleG"
                :observed-gradient="observedGradient"
                :observed-gradient-pct="observedGradientPct"
              />
            </v-expansion-panel-text>
          </v-expansion-panel>
        </v-expansion-panels>
      </div>
    </v-responsive>
  </v-container>
</template>

<style>
.handwriting {
  font-family: "Handwriting" !important;
}
s,
strike {
  text-decoration: none;
  position: relative;
  display: inline-block;
}
s::before,
strike::before {
  top: 50%; /*tweak this to adjust the vertical position if it's off a bit due to your font family */
  background: red; /*this is the color of the line*/
  opacity: 0.7;
  content: "";
  width: 110%;
  position: absolute;
  height: 0.1em;
  border-radius: 0.1em;
  left: -5%;
  white-space: nowrap;
  display: block;
  transform: rotate(-15deg);
}
s.straight::before,
strike.straight::before {
  transform: rotate(0deg);
  left: -1%;
  width: 102%;
}
math {
  width: 100%;
  margin-bottom: 8px;
  overflow-x: scroll;
}
math::-webkit-scrollbar {
  display: none;
}
mtable {
  width: 100%;
}
mtd {
  padding: 5px;
}
mtd:nth-child(3) {
  text-align: left;
  width: 85%;
}
</style>

<script setup lang="ts">
import { reactive } from "vue";
import { computed, ref } from "vue";

import MathCalcs from "@/components/MathCalcs.vue";
import Diagram from "@/components/Diagram.vue";

const toRad = (deg: number) => deg * (Math.PI / 180);
const toDeg = (rad: number) => rad * (180 / Math.PI);
const angleA1 = ref(0.955);
const angleA2 = ref(21.36);
const sideB = ref(51.369);
const sideC = ref(21.97);

const angleARad = computed(() => toRad(angleA1.value) + toRad(angleA2.value));
const sideA = computed(() =>
  Math.sqrt(
    sideB.value ** 2 +
      sideC.value ** 2 -
      2 * sideB.value * sideC.value * Math.cos(angleARad.value)
  )
);
const angleC = computed(() =>
  toDeg(
    Math.acos(
      (sideA.value ** 2 + sideB.value ** 2 - sideC.value ** 2) /
        (2 * sideA.value * sideB.value)
    )
  )
);
const angleB = computed(() =>
  toDeg(
    Math.acos(
      (sideA.value ** 2 + sideC.value ** 2 - sideB.value ** 2) /
        (2 * sideA.value * sideC.value)
    )
  )
);
const angleG = computed(() =>
  angleA1.value < 0
    ? 180 - angleA2.value - angleB.value
    : angleA1.value + angleC.value
);
const observedGradient = computed(() => Math.tan(toRad(angleG.value)));
const observedGradientPct = computed(() => observedGradient.value * 100);
const valid = ref(true);
</script>
