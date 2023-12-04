<script setup lang="ts">
import { computed, ref } from "vue";
const restTime = ref(0);

const restTimeStep = computed(function () {
  return restTime.value < 60 ? 5 : 10;
});

const formattedRestTime = computed(() => {
  const newRestTime = restTime.value;

  if (isNaN(newRestTime)) {
    return "Invalid Time";
  } else if (newRestTime < 60) {
    return newRestTime + "s";
  } else {
    const minutes = Math.floor(newRestTime / 60);
    const seconds = newRestTime % 60;
    return `${minutes}m ${seconds}s`;
  }
});

function updateFormattedRestTime(formattedRestTime: any) {
  const formattedRestTimeString = formattedRestTime;
  let mm = null;
  let ss = null;
  let minutes = 0;
  let seconds = 0;

  try {
    [, mm, ss] = formattedRestTimeString.match(/^(\d*)m (\d*)s$/);
  } catch {}
  try {
    [, ss] = formattedRestTimeString.match(/^(\d*)s$/);
  } catch {}

  if (mm) {
    minutes = parseInt(mm);
  }
  if (ss) {
    seconds = parseInt(ss);
  }

  restTime.value = minutes * 60 + seconds;
}
</script>


<!-- Slider intervals definition: 
Range: 0s (off) to 10m, 
Intervals: 
  1 x 0, (0s)
  12 x 5s, (Every 5s to 1min),
  54 x 10s, (Every 10s to 10min)

Total Intervals: (1+12+54 = 67)
 -->
<template>
  <v-row class="mt-1">
    <v-col cols="9">
      <v-slider
        v-model="restTime"
        color="primary"
        max="600"
        min="0"
        :step="restTimeStep"
        hide-details
      ></v-slider>
    </v-col>

    <v-col cols="3">
      <v-text-field
        v-model="formattedRestTime"
        color="primary"
        variant="outlined"
        label="Rest"
        @update:model-value="updateFormattedRestTime"
      >
      </v-text-field>
    </v-col>
  </v-row>
</template>
