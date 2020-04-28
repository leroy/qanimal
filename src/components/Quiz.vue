<template>
	<div class="flex flex-col h-screen">
		<input type="text" placeholder="typ je antwoord" class="text-xl border-4 border-transparent" :class="{'border-red-400': wrong}" @keydown.enter="answer">
		<div v-if="image" class="w-full h-full bg-contain bg-no-repeat bg-center" :style="{'background-image': `url('${image}')`}"></div>
	</div>
</template>

<script>
	export default {
		props: {
			questions: Object
		},

		data() {
			return {
				current: null,
				wrong: false
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
			},
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
					this.wrong = false;
					return;
				}

				e.target.value = '';
				this.wrong = true;
			}
		}
	}
</script>