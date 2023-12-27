<template>
  <math display="block">
    <mtable>
      <mtr>
        <mtd>
          <msub>
            <mi>A</mi>
            <mi>1</mi>
          </msub>
        </mtd>
        <mtd>
          <mo>=</mo>
        </mtd>
        <mtd>
          <mn>{{ angleA1.toFixed(4) }}</mn>
          <mtext>°</mtext>
        </mtd>
      </mtr>
      <mtr>
        <mtd>
          <msub>
            <mi>A</mi>
            <mi>2</mi>
          </msub>
        </mtd>
        <mtd>
          <mo>=</mo>
        </mtd>
        <mtd>
          <mn>{{ angleA2.toFixed(4) }}</mn>
          <mtext>°</mtext>
        </mtd>
      </mtr>
      <mtr>
        <mtd>
          <msub>
            <mi>Side</mi>
            <mi>b</mi>
          </msub>
        </mtd>
        <mtd>
          <mo>=</mo>
        </mtd>
        <mtd>
          <mn>{{ sideB.toFixed(4) }}</mn>
          <mtext>m</mtext>
        </mtd>
      </mtr>
      <mtr>
        <mtd>
          <msub>
            <mi>Side</mi>
            <mi>c</mi>
          </msub>
        </mtd>
        <mtd>
          <mo>=</mo>
        </mtd>
        <mtd>
          <mn>{{ sideC.toFixed(4) }}</mn>
          <mtext>m</mtext>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <math display="block">
    <mtable>
      <mtr>
        <mtd>
          <msub>
            <mi>Side</mi>
            <mi>a</mi>
          </msub>
        </mtd>
        <mtd>
          <mo>=</mo>
        </mtd>
        <mtd>
          <msqrt>
            <msup>
              <mi>b</mi>
              <mn>2</mn>
            </msup>
            <mo>+</mo>
            <msup>
              <mi>c</mi>
              <mn>2</mn>
            </msup>
            <mo>-</mo>
            <mn>2</mn>
            <mi>b</mi>
            <mi>c</mi>
            <mo>·</mo>
            <mi>cos(</mi>
            <msub>
              <mi>A</mi>
              <mi>1 </mi>
            </msub>
            <mo>+</mo>
            <msub>
              <mi>A</mi>
              <mi>2</mi>
            </msub>
            <mi>)</mi>
          </msqrt>
        </mtd>
      </mtr>
      <mtr>
        <mtd> </mtd>
        <mtd>
          <mo>=</mo>
        </mtd>
        <mtd>
          <msqrt>
            <msup>
              <mn>({{ sideB.toFixed(4) }})</mn>
              <mn>2</mn>
            </msup>
            <mo>+</mo>
            <msup>
              <mn>({{ sideC.toFixed(4) }})</mn>
              <mn>2</mn>
            </msup>
            <mo>-</mo>
            <mn>2</mn>
            <mn>({{ sideB.toFixed(4) }})</mn>
            <mn>({{ sideC.toFixed(4) }})</mn>
            <mo>·</mo>
            <mi>cos(</mi>
            <mn>{{ angleA1.toFixed(4) }}</mn>
            <mo>+</mo>
            <mn>{{ angleA2.toFixed(4) }})</mn>
          </msqrt>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>

        <mtd>
          <mo>=</mo>
        </mtd>

        <mtd>
          <mn>{{ sideA.toFixed(4) }}m</mn>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <math display="block" v-if="angleA1 >= 0">
    <mtable>
      <mtr>
        <mtd>C</mtd>
        <mtd>=</mtd>
        <mtd>
          <mi>acos</mi>
          <mo>(</mo>
          <mfrac>
            <mrow>
              <msup>
                <mn>a</mn>
                <mn>2</mn>
              </msup>
              <mo>+</mo>
              <msup>
                <mn>b</mn>
                <mn>2</mn>
              </msup>
              <mo>-</mo>
              <msup>
                <mn>c</mn>
                <mn>2</mn>
              </msup>
            </mrow>
            <mrow>
              <mn>2</mn>
              <mo>·</mo>
              <mi>ba</mi>
            </mrow>
          </mfrac>
          <mo>)</mo>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mi>acos</mi>
          <mo>(</mo>
          <mfrac>
            <mrow>
              <msup>
                <mn>({{ sideA.toFixed(4) }})</mn>
                <mn>2</mn>
              </msup>
              <mo>+</mo>
              <msup>
                <mn>({{ sideB.toFixed(4) }})</mn>
                <mn>2</mn>
              </msup>
              <mo>-</mo>
              <msup>
                <mn>({{ sideC.toFixed(4) }})</mn>
                <mn>2</mn>
              </msup>
            </mrow>
            <mrow>
              <mn>2</mn>
              <mn>({{ sideA.toFixed(4) }})</mn>
              <mn>({{ sideB.toFixed(4) }})</mn>
            </mrow>
          </mfrac>
          <mo>)</mo>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>{{ angleC.toFixed(4) }}</mn>
          <mtext>°</mtext>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <math display="block" v-else>
    <mtable>
      <mtr>
        <mtd>B</mtd>
        <mtd>=</mtd>
        <mtd>
          <mi>acos</mi>
          <mo>(</mo>
          <mfrac>
            <mrow>
              <msup>
                <mn>a</mn>
                <mn>2</mn>
              </msup>
              <mo>+</mo>
              <msup>
                <mn>c</mn>
                <mn>2</mn>
              </msup>
              <mo>-</mo>
              <msup>
                <mn>b</mn>
                <mn>2</mn>
              </msup>
            </mrow>
            <mrow>
              <mn>2</mn>
              <mo>·</mo>
              <mi>ac</mi>
            </mrow>
          </mfrac>
          <mo>)</mo>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mi>acos</mi>
          <mo>(</mo>
          <mfrac>
            <mrow>
              <msup>
                <mn>({{ sideA.toFixed(4) }})</mn>
                <mn>2</mn>
              </msup>
              <mo>+</mo>
              <msup>
                <mn>({{ sideC.toFixed(4) }})</mn>
                <mn>2</mn>
              </msup>
              <mo>-</mo>
              <msup>
                <mn>({{ sideB.toFixed(4) }})</mn>
                <mn>2</mn>
              </msup>
            </mrow>
            <mrow>
              <mn>2</mn>
              <mn>({{ sideA.toFixed(4) }})</mn>
              <mn>({{ sideC.toFixed(4) }})</mn>
            </mrow>
          </mfrac>
          <mo>)</mo>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>{{ angleB.toFixed(4) }}</mn>
          <mtext>°</mtext>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <math display="block" v-if="angleA1 >= 0">
    <mtable>
      <mtr>
        <mtd>
          <msub>
            <mi>y</mi>
            <mi></mi>
          </msub>
        </mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <msub>
            <mi>A</mi>
            <mi>1</mi>
          </msub>
        </mtd>
      </mtr>
      <mtr>
        <mtd>
          <mo>∴</mo>
          <mi>G</mi>
        </mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mi>X</mi>
          <mo>=</mo>
          <msub>
            <mi>A</mi>
            <mi>1</mi>
          </msub>
          <mo>+</mo>
          <mi>C</mi>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mo>(</mo>
          <mn>{{ angleA1.toFixed(4) }}</mn>
          <mo>+</mo>
          <mn>{{ angleC.toFixed(4) }}</mn>
          <mo>)</mo>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>{{ angleG.toFixed(4) }}</mn>
          <mtext>°</mtext>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <math display="block" v-else>
    <mtable>
      <mtr>
        <mtd>
          <msub>
            <mi>y</mi>
            <mi></mi>
          </msub>
        </mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <msub>
            <mi>A</mi>
            <mi>2</mi>
          </msub>
        </mtd>
      </mtr>
      <mtr>
        <mtd>
          <mo>∴</mo>
          <mi>X</mi>
        </mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>180</mn>
          <mo>-</mo>
          <msub>
            <mi>A</mi>
            <mi>2</mi>
          </msub>
          <mo>-</mo>
          <mi>B</mi>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>180</mn>
          <mo>-(</mo>
          <mn>{{ angleA2.toFixed(4) }}</mn>
          <mo>+</mo>
          <mn>{{ angleB.toFixed(4) }}</mn>
          <mo>)</mo>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>{{ angleG.toFixed(4) }}</mn>
          <mtext>°</mtext>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <math display="block">
    <mtable>
      <mtr>
        <mtd><mi>ObsG</mi></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mi>tan(</mi>
          <mi>X</mi>
          <mi>)</mi>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mi>tan(</mi>
          <mn>{{ angleG.toFixed(4) }}</mn>
          <mi>)</mi>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>{{ observedGradient.toFixed(5) }}</mn>
        </mtd>
      </mtr>
      <mtr>
        <mtd></mtd>
        <mtd><mo>=</mo></mtd>
        <mtd>
          <mn>{{ observedGradientPct.toFixed(2) }}%</mn>
        </mtd>
      </mtr>
    </mtable>
  </math>
  <p class="text-caption">
    Note: In between steps are shown rounded for brevity but are not actually
    rounded until the end
  </p>
</template>
<script setup lang="ts">
import { defineProps } from "vue";
defineProps<{
  angleA1: number;
  angleA2: number;
  sideB: number;
  sideC: number;
  angleARad: number;
  sideA: number;
  angleC: number;
  angleB: number;
  angleG: number;
  observedGradient: number;
  observedGradientPct: number;
}>();
</script>
