<template>
  <div>
    <div class="container border p-3 shadow rounded">
      <div class="progress shadow rounded" style="height: 30px">
        <div
          class="progress-bar shadow rounded"
          role="progressbar"
          aria-valuemin="0"
          aria-valuemax="120"
          style="color: #000; font-weight: 800"
          :value="bmi"
          :style="{
            background: activeColor,
            width: bmi + '%',
          }"
        >
          {{ message + " " + bmi }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["bmi", "activeColor", "isHidden", "message"],
};
</script>

<style></style>
