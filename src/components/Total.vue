<template>
  <div class="total">
    <div class="total__title">Стоимость</div>
    <div class="total__value">{{ total }} Р<span class="ruble-stroke_regular">–</span></div>
  </div>
</template>

<script>
export default {
  name: 'Total',
  props: {
    total: Number
  }
}
</script>