<template>
  <div class="content__category">
    <div class="category">
      <div class="category__title">{{ category.categoryTitle }}<div class="category__price">{{ price }}<span v-if="category.price">–</span></div></div>
      <div class="category__list">
        <div class="category-list">
          <Page
            v-for="(item, index) in category.items"
            :page="item"
            :pageId="index"
            :catId="catId"
            :radioButton="category.radioButton"
            :styles="styles"
            :key="index"
            @add="$emit('add', $event)"
            @detailed="$emit('detailed', $event)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Page from './Page.vue'

export default {
  name: 'Category',
  props: {
    category: Object,
    catId: Number,
    styles: Object
  },
  components: {
    Page
  },
  computed: {
    price: function () {
      let price = this.category.price ? '+' + this.category.price + ' Р' : 'Базовый набор'
      return price
    }
  }
}
</script>