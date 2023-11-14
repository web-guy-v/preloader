<script setup>
	import gsap from 'gsap'
	import { general } from '@/store/index.js'

	watch(() => general.isPreloaderVisible, (val) => {
		if(!val) {
			gsap.from('.gallery', {
				scale: 1.1,
				opacity: 0.2,
				duration: 1,
				delay: 0.1
			})
		}
	})

	const images = [
		'1.jpg', '2.jpg', '3.jpg', '4.jpg', '5.jpg',
		'6.jpg', '7.jpg', '8.jpg', '9.jpg', '10.jpg',
		'11.jpg', '12.jpg',
	]
</script>
<template>
	<div class="gallery">

		<div
			v-for="_ in 10"
			class="gallery__wrap"
		>

			<div
				v-for="img in images"
				class="gallery__item"
			>
				<img
					:src="img"
					class="gallery__img"
				/>
			</div>

		</div>

	</div>
</template>
<style lang='scss' scoped>

.gallery {
	will-change: transform, opacity;
}
.gallery__wrap {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
}
.gallery__item {
	height: 20vw;
}
.gallery__img {
	vertical-align: top;
	width: 100%;
	height: 100%;
	object-fit: cover;
	object-position: center;
}

</style>