<template>
	<div class="detailed" @click="$emit('closeDetailed')">
		<div class="detailed__content">
			<div class="detailed-content" onclick="event.stopPropagation()">
				<div class="detailed-content__picture">
					<div class="detailed-picture">
						<div class="detailed-picture__front-side">
							<img :src="require('./../assets/images/pages/' + page.images.front)" alt="" class="detailed-picture__image">
						</div>
						<div class="detailed-picture__back-side">
							<img :src="require('./../assets/images/pages/' + page.images.back)" alt="" class="detailed-picture__image">
						</div>
					</div>
				</div>
				<div class="detailed-content__data">
					<div class="detailed-content__name">{{ page.title }}</div>
					<div class="detailed-content__description">{{ page.description }}</div>
					<div class="detailed-content__price">{{ page.price }} Р<span>–</span></div>
				</div>
				<div class="detailed-content__add">
					<div :class="['detailed-content__button', page.added ? 'detailed-content__button_remove' : false]" @click="$emit('add', {pageId: id.pageId, catId: id.catId})">{{ page.added ? 'Удалить' : 'Добавить' }}</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'PageDetailed',
  props: {
    page: Object,
    id: Object
  }
}
</script>