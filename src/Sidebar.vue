<template>
	<aside class="sm-side">
		<div class="user-head">
			<img src="src/assets/images/picture.jpg" width="50" height="50" />

			<div class="user-name">
				<h5>Liraj Maharjan</h5>
				<span class="email-address">info@codingpractice.com</span>
			</div>
		</div>

		<div class="compose-wrapper">
			<appCompose></appCompose>
		</div>

		<ul class="inbox-nav">
			<li :class="{active: activeView == 'app-inbox'}">
				<a href="#" @click.prevent="navigate('app-inbox', 'Inbox')">
					<i class="fa fa-inbox"></i> Inbox  <span class="badge badge-danger pull-right">{{ unreadMessages.length }}</span>
				</a>
			</li>

			<li :class="{active: activeView == 'app-sent'}">
				<a href="#"  @click.prevent="navigate('app-sent', 'Sent')">
					<i class="fa fa-envelope"></i> Sent <span class="badge badge-info pull-right">{{ sentMessages.length }}</span>
				</a>
			</li>
			<li :class="{ active: activeView == 'app-trash'}">
				<a href="#"  @click.prevent="navigate('app-important', 'Important')">
					<i class="fa fa-bookmark"></i> Important <span class="badge badge-warning pull-right">{{ importantMessages.length }}</span>
				</a>
			</li>
			<li :class="{ active: activeView == 'app-trash' }">
				<a href="#"  @click.prevent="navigate('app-Trash', 'Trash')">
					<i class="fa fa-trash"></i> Trash <span class="badge badge-infp pull-right">{{ trashedMessages.length }}</span>
				</a>
			</li>
		</ul>
	</aside>
</template>

<script>
	import { eventBus } from './main';
	import Compose from './Compose.vue'

	export default {
		props: {
			messages: {
				type: Array,
				required: true
			}
		},
		created() {
			eventBus.$on('changeView', (data) => {
				this.activeView = data.tag;
			});
		},
		data() {
			return {
				activeView: 'app-inbox'
			};
		},
		methods: {
			navigate(newView, title){
			eventBus.$emit('changeView', {
				tag: newView,
				title: title
			});
			}
		},
		computed: {
			unreadMessages() {
				return this.messages.filter(function(message){
					return (message.type == 'incoming' && !message.isRead && !message.isDeleted);
				});
			},
			sentMessages() {
				return this.messages.filter(function(message){
					return (message.type == 'outgoing' && !message.isDeleted);
				});
			},
			importantMessages () {
				return this.messages.filter(function(message){
					return (message.type == 'incoming' && message.isImportant === true && !message.isDeleted);
				});
			},
			trashedMessages () {
				return this.messages.filter(function(message){
					return message.isDeleted === true;
				});
			}
		},
		components: {
			appCompose: Compose
		}
	}
</script>
