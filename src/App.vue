<template>
  <div class="container">
    <div class="mail-box">
      <appSidebar :messages="messages"></appSidebar>
      <appContent :messages="messages"></appContent>
    </div>
  </div>
</template>

<script>
  import Sidebar from './Sidebar.vue';
  import Content from './Content.vue';
  import messages from './data/messages.js'; 
  import randomMessages from './data/random-messages'
  import { eventBus } from './main'

  export default {
      data() {
        return {
          messages: messages
        };
      },
      created() {
        eventBus.$on('sentMessages', (data) => {
          let temp = [data.message];
          this.messages = temp.concat(this.messages.slice(0));
        });

        eventBus.$on('refreshMessages', () => {
                let randomIndex = Math.floor(Math.random() * randomMessages.length);
                let temp = [randomMessages[randomIndex]];
                this.messages = temp.concat(this.messages.slice(0));
            }); 
      },
      components: {
        appSidebar: Sidebar,
        appContent: Content,
      }
  }
</script>