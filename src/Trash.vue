<template>
	<div class="inbox-body">
		<appTrash :messages="trashedMessages"></appTrash>
	</div>
</template>

<script>
	import Messages from './Messages.vue';

	export default {
		props: {
			data: {
				type: Object,
				required: true
			}
		},
		computed: {
			trashedMessages () {
				return this.data.messages.filter(function(message){
					return message.isDeleted === true;
				});
			}
		},
		components: {
			appTrash: Messages
		}
	}
</script>