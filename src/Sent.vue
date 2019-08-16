<template>
<div>
	<div class="inbox-body">
		<appMessages :messages="sentMessages"></appMessages>
	</div>
</div>
</template>

<script>
	import Messages from './Messages.vue'

	export default {
		props: {
			data: {
				type: Object,
				requred: true
			}
		},
		computed: {
			sentMessages() {
				return this.data.messages.filter(function(message){
					return (message.type == 'outgoing' && !message.isDeleted);
				});
			},
		},
		components: {
			appMessages: Messages
		}
	}
</script>