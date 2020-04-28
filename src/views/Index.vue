<template>
	<upload v-if="Object.keys(images).length === 0" @change="addImages"></upload>
	<quiz v-else :questions="images"></quiz>
</template>

<script>
	import Upload from "@/components/Upload";
	import Quiz from "@/components/Quiz";

	export default {
		components: {
			Upload,
			Quiz
		},

		data() {
			return {
				images: {}
			}
		},

		methods: {
			addImages(e)
			{
				this.images = e.images;
			}
		}
	}
</script>