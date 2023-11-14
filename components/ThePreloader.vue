<script lang="ts" setup>

	import { gsap } from 'gsap'

	const DELAY_BETWEEN_PHOTO_LOADED = 15

	const number_of_images_loaded = ref(0)
	const total_images = ref(0)
	const image_index = ref(0)

	onMounted(() => {

		nextTick(() => {
			setTimeout(async () => {
				await document.fonts.load

				gsap.to('.preloader__percent', {
					opacity: 1,
					duration: 0.2
				})

				gsap.set('body', {
					overflow: 'hidden'
				})

				loadNextImage()
			}, 0)
		})
	})

	function setProgress(total: number) {
		number_of_images_loaded.value++
		total_images.value = total
	}

	function loadNextImage() {
		const images = document.querySelectorAll('img');

		if (image_index.value < images.length) {
			const img = images[image_index.value]
			if (img.complete) {
				setProgress(images.length)
				image_index.value++
				setTimeout(loadNextImage, DELAY_BETWEEN_PHOTO_LOADED);
			} else {
				img.onload = () => {
					setProgress(images.length)
					image_index.value++
					setTimeout(loadNextImage, DELAY_BETWEEN_PHOTO_LOADED)
				}
			}
		}
	}


	const progress = computed(() => {
		return Math.min(Math.floor(number_of_images_loaded.value / total_images.value * 100), 100)
	})

	watch(() => progress.value, (number) => {
		if(number === 100) {


			gsap.fromTo('.preloader', {
				clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)'
			}, {
				clipPath: 'polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%)',
				duration: 0.7,
				onComplete() {
					gsap.set('body', {
						clearProps: 'all'
					})
				}
			})
		}
	})


</script>
<template>
	<div class="preloader">
		<div class="preloader__percent h3">
			{{ progress ? progress : 0 }}%
		</div>
	</div>
</template>
<style lang='scss' scoped>
.preloader {
	position: fixed;
	inset: 0;
	z-index: 9999;
	background: black;
	color: white;
	display: flex;
	align-items: center;
	justify-content: center;
}
.preloader__percent {
	opacity: 0;
	font-size: 80px;
}
</style>