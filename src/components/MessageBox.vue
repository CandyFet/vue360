<template>
<div>
  <h1>Project Twitter Box Client</h1>
  <div class="message_area">
    <div v-if="checkRemainingCharacters()">
      <textarea v-model="message" cols="30" rows="10"></textarea>
      <button v-on:click="createMessage" type="submit">Submit</button> <br>
      <span>{{ remainingCharacters() }} characters left</span>
    </div>
    <div v-else>
      <textarea v-model="message" cols="30" rows="10"></textarea>
      <button :disabled="true" type="submit">Submit</button> <br>
      <span>Maximum tweet characters is {{tweetMaxLength}}</span>
    </div>
  </div>
  <div v-for="tweet in messageList.length" :key="tweet">
    <Message :msg="messageList[tweet-1]" />
  </div>
</div>
</template>

<script>
import Message from './Message'
export default {
  name: 'MessageBox',
  data() {
    return {
      message: '',
      messageList: [],
      tweetMaxLength: 280,
    }
  },
  components: {
    Message
  },
  methods: {
    checkRemainingCharacters() {
      return this.message.length < this.tweetMaxLength
    },
    remainingCharacters() {
      return this.tweetMaxLength - this.message.length
    },
    createMessage(event) {
      event.preventDefault();
      this.messageList.push(this.message)
    }
  }
}
</script>

<style scoped>

</style>
