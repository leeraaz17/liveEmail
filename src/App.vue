<template>
  <div class="container">
    <div class="mail-box">
      <appSidebar :messages="messages"></appSidebar>
      <appContent></appContent>
    </div>
  </div>
</template>

<script>
  import Sidebar from './Sidebar.vue';
  import Content from './Content.vue';
  import messages from './data/messages'; 

  export default {
      data() {
        return {
          messages: messages
        };
      },
      components: {
        appSidebar: Sidebar,
        appContent: Content,
      }
  }
</script>