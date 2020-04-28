<template>
	<div>
		<img v-if="image" :src="image">

		<input type="text" @keydown.enter="answer">
	</div>
</template>

<script>
	export default {
		props: {
			questions: Object
		},

		data() {
			return {
				current: null
			}
		},

		mounted()
		{
			this.nextQuestion();
		},

		computed: {
			names() {
				return Object.keys(this.questions);
			},

			name() {
				return this.current.split('.').slice(0, -1).join('.');
			},

			image() {
				if (!this.current) return null;

				return this.questions[this.current];
			}
		},

		methods: {
			nextQuestion() {
				this.current = this.names[~~(Math.random() * this.names.length)];
			},

			answer(e)
			{
				if (e.target.value === this.name) {
					e.target.value = '';
					this.nextQuestion();
				}
			}
		}
	}
</script>