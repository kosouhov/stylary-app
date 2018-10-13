<template>
  <div class="category-list__planner-page" :style="styles.plannerPage">
    <div class="planner-page">
      <div class="planner-page__picture" @click="$emit('detailed', {pageId: pageId, catId: catId})">
        <div class="planner-page__images">
          <div class="planner-page__front-side"><img :src="require('./../assets/images/pages/' + page.images.front)" class="planner-page__image"></div>
          <div class="planner-page__back-side"><img :src="require('./../assets/images/pages/' + page.images.back)" class="planner-page__image"></div>
        </div>
        <div :class="['planner-page__buttons', page.added ? 'added' : false]">
          <div class="planner-page__icons" @click="$emit('add', {pageId: pageId, catId: catId})" onclick="event.stopPropagation()">
            <img src="./../assets/images/add.svg" class="planner-page__add" :class="page.radio ? 'planner-page__add_radio' : false">
            <img src="./../assets/images/remove.svg" class="planner-page__remove" v-if="!page.radio">
          </div>
        </div>
      </div>
      <div class="planner-page__data">
        <div class="planner-page__name">{{ page.title }}</div>
        <div class="planner-page__description">{{ page.description }}</div>
        <div class="planner-page__price" v-if="page.price">{{ page.price }} P<span>–</span></div>
        <div class="planner-page__price planner-page__price_base" v-else>Базовый набор</div>
      </div>
      <div class="planner-page__status" v-if="page.added"><img src="./../assets/images/tick.svg" class="planner-page__added-icon"></div>
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