<template>
	<div>
		<input type="file" @change="change" multiple>
	</div>
</template>

<script>
	export default {
		methods: {
			change(e)
			{
				let images = {};

				let files = e.target.files;
				let filesRead = 0;

				for (let i = 0; i < files.length; i++) {
					let reader = new FileReader();

					reader.onload = (event) => {
						filesRead++;
						images[files[i].name] = event.target.result;

						if (filesRead === files.length) {
							e.target.value = '';
							this.$emit('change', {images});
						}
					};

					reader.readAsDataURL(files[i]);
				}

			},
		}
	}
</script>