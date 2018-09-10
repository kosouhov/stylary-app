<template>
  <div class="sidebar">
    <div class="sidebar__header"></div>
    <div class="sidebar__switch">
      <div
        :class="['switch', night]"
        @click="change('night')"
      >
        <div class="switch__on"><img src="./../assets/images/moon.svg" class="switch__image"></div>
        <div class="switch__off"><img src="./../assets/images/sun.svg" class="switch__image"></div>
      </div>
    </div>
    <div class="sidebar__switch">
      <div
        :class="['switch', largeGrid]"
        @click="change('largeGrid')"
      >
        <div class="switch__on"><img src="./../assets/images/grid2x2.svg" class="switch__image"></div>
        <div class="switch__off"><img src="./../assets/images/grid3x3.svg" class="switch__image"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  data() {
    return {
      night: false,
      largeGrid: false,
    }
  },
  props: {
    mode: Object
  },
  methods: {
    change: function(event) {
      this.$emit('changeMode', event);
      (this[event] == 'mode-on') ? this[event] = 'mode-off' : this[event] = 'mode-on'
    }
  }
}
</script>