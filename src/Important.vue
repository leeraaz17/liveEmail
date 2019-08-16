<template>
	<div class="inbox-body">
		<appImportant :messages="importantMessages"></appImportant>
	</div>
</template>

<script>
	import Messages from './Messages.vue'

	export default {
		props: {
			data: {
				type: Object,
				required: true
			}
		},
		computed: {
			importantMessages() {
				return this.data.messages.filter(function(message){
					return (message.type == 'incoming' && message.isImportant === true);
				});
			},
		},
		components: {
			appImportant: Messages
		}
	}
</script>