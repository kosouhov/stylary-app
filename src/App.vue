<template>
  <div id="app">
    <div :class="['page', mode, detailed.show ? 'page_blurred' : false]" @click="mode.mobileMenu = false">
      <div class="page__sidebar">
        <Sidebar
          :mode="mode"
          @changeMode="changeMode($event)"
        />
      </div>
      <div class="page__main">
        <div class="main">
          <div class="main__header">
            <div class="header">
              <div class="header__logo">
                <div class="logo">
                  <div class="logo__type">Stylary</div>
                  <div class="logo__subtitle">конструктор</div>
                </div>
              </div>
              <div class="header__menu" onclick="event.stopPropagation()">
                <div class="menu-container">
                  <ul :class="['menu', mode.mobileMenu ? 'opened' : false]">
                    <li class="menu__item"><a href="https://github.com/kosouhov/stylary-app" class="menu__link">О проекте</a></li>
                    <li class="menu__item"><a href="mailto:vladimir@kosouhov.com" class="menu__link">Связаться с нами</a></li>
                  </ul>
                </div>
                <div class="open-menu" @click="mode.mobileMenu = true">
                  <div class="open-menu__icon"><img src="./assets/images/menu.svg" class="open-menu__image"></div>
                  <div class="open-menu__type">меню</div>
                </div>
              </div>
            </div>
          </div>
          <div class="main__content">
            <div class="content" ref="content">
              <Category
                v-for="(item, index) in pages"
                :category="item"
                :catId="index"
                :styles="styles"
                :key="index"
                @add="add($event)"
                @detailed="showDetailed(true, $event)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <PageDetailed
      v-if="detailed.show"
      :page="pages[detailed.id.catId].items[detailed.id.pageId]"
      :id="detailed.id"
      @add="add($event)"
      @closeDetailed="detailed.show = false"
    />
    <Total
      :total="totalPrice"
    />
  </div>
</template>

<script>
import Category from './components/Category.vue'
import Sidebar from './components/Sidebar.vue'
import PageDetailed from './components/PageDetailed.vue'
import Total from './components/Total.vue'
import Data from './assets/data.json'

export default {
  name: 'app',
  components: {
    Category,
    Sidebar,
    PageDetailed,
    Total
  },
  data() {
    return {
      pages: Data,
      mode: {
        night: false,
        largeGrid: false,
        mobileMenu: false
      },
      styles: {
        plannerPage: {
          'max-width': 0
        }
      },
      detailed: {
        show: false,
        id: {
          pageId: 0,
          catId: 0
        }
      }
    }
  },
  methods: {
    add: function(event) {
      let ts = this,
          page = ts.pages[event.catId].items[event.pageId]
      if (page.set_id) { //страница в наборе
        if (page.radio) { //страница в наборе радиокнопок
          ts.pages.forEach(function(category, cat_id) {
            category.items.forEach(function(item, item_id) {
              if (item.set_id == page.set_id) {
                if (item.radio) {
                  item.added = false
                }
              }
            })
          })
          page.added = true
        } else {
          ts.pages.forEach(function(category, cat_id) {
            category.items.forEach(function(item, item_id) {
              if (item.set_id == page.set_id) {
                item.added = !item.added
              }
            })
          })
        }
      } else { //одиночная страница
        page.added = !page.added
      }
    },
    showDetailed: function(show, id) {
      this.detailed.show = show
      this.detailed.id = id
    },
    changeMode: function(mode) {
      this.mode[mode] = !this.mode[mode]
      this.setPlannerPageStyle()
    },
    setPlannerPageStyle: function() {
      let contentWidth = this.$refs.content.querySelector('.category').getBoundingClientRect().width,
          pagesInRow = Math.floor(contentWidth / this.getPageMinWidth())
      this.styles.plannerPage['max-width'] = pagesInRow ? contentWidth / pagesInRow + 'px' : contentWidth + 'px'
    },
    getPageMinWidth: function() {
      return ((document.body.clientWidth <= 480) || (this.mode.largeGrid)) ? 400 : 200
    }
  },
  computed: {
    totalPrice: function () {
      let T = {},
          total = 0
      this.pages.forEach(function(category, cat_id) {
        category.items.forEach(function(item, item_id) {
          if (item.set_id) {
            item.added ? T[item.set_id] = item.price : false
          } else {
            item.added ? T[cat_id + '-' + item_id] = item.price : false
          }
        })
      })
      for (let i in T) {
        total += T[i]
      }
      return total
    }
  },
  mounted: function() {
    this.$nextTick(function() {
      window.addEventListener('resize', this.setPlannerPageStyle)
      this.setPlannerPageStyle()
    })
  }
}
</script>

<style lang="sass">
  @import './assets/style.sass'
</style>