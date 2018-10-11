<template>
  <div class="category-list__planner-page" :style="styles.plannerPage">
    <div class="planner-page">
      <div class="planner-page__picture" @click="$emit('detailed', {pageId: pageId, catId: catId})">
        <div class="planner-page__images">
          <div class="planner-page__front-side"><img :src="require('./../assets/images/pages/' + page.images.front)" class="planner-page__image"></div>
          <div class="planner-page__back-side"><img :src="require('./../assets/images/pages/' + page.images.back)" class="planner-page__image"></div>
        </div>
        <div :class="['planner-page__buttons', page.added ? 'added' : false]">
          <div class="planner-page__icons" @click="$emit('add', {pageId: pageId, catId: catId})" onclick="event.stopPropagation()"><img src="./../assets/images/add.svg" class="planner-page__add"><img src="./../assets/images/remove.svg" class="planner-page__remove"></div>
        </div>
      </div>
      <div class="planner-page__data">
        <div class="planner-page__name">
          <div class="planner-page__name-container">{{ page.title }}<img src="./../assets/images/tick.svg" class="planner-page__added-icon" v-if="page.added"></div>
        </div>
        <div class="planner-page__description">{{ page.description }}</div>
      </div>
      <div class="planner-page__status"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Page',
  props: {
    page: Object,
    pageId: Number,
    catId: Number,
    styles: Object
  }
}
</script>