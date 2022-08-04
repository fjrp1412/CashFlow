<template>
  <div>
    <svg viewBox="0 0 300 200">
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        :y1="zero"
        x2="300"
        :y2="zero"
      />
      <polyline
        fill="none"
        stroke="#0689B0"
        stroke-width="2"
        :points="points"
      />
    </svg>
    <p>Ultimos 30 dias</p>
  </div>
</template>

<script setup>
import { toRefs, defineProps, computed } from "vue";

const props = defineProps({
  amounts: {
    type: Array,
    default: () => [],
  },
});

const { amounts } = toRefs(props);

const amountToPixels = (amount) => {
  const min = Math.min(...amounts.value);
  const max = Math.max(...amounts.value);

  const amountAbs = amount + Math.abs(min);
  const minmax = Math.abs(max) + Math.abs(min);

  return 200 - ((amountAbs * 100) / minmax) * 2;
};

const zero = computed(() => amountToPixels(0));

const points = computed(() => {
  const total = amounts.value.length;
  return amounts.value.reduce((points, amount, idx) => {
    const x = (300 / total) * (idx + 1);
    const y = amountToPixels(amount);
    return `${points} ${x},${y}`;
  }, "0, 100");
});

console.log(amounts.value);
</script>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
