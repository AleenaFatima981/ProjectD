<template>
  <section class="home-page">
    <div class="profile-circle">
      <img src="https://th.bing.com/th/id/OIP.kvKHlMN7XZ3BHQq3s4WZbwAAAA?pid=ImgDet&rs=1" alt="Your Name">
    </div>
    <div class="home-content">
      <h1>Welcome to BAKE IT!</h1>
    </div>
    <h2> AI Customer Service </h2>
    <div class="chatbox">
      <div v-for="message in messages">
        <strong v-if="message.sender==='user'">You: </strong>
        <strong v-if="message.sender==='ai'">AI: </strong>
        {{ message.content }}
      </div>
    </div>
    <div>
      <input v-model="userMessage" type="text" placeholder="Ask BakeIT bot..." @keyup.enter="sendMessage">
      <button @click="sendMessage">Send</button>
    </div>
  </section>
</template>

<script>

export default {
  data() {
    return {
      userMessage: '',
      messages: [],
      myTrack : new Audio ('assets/notifications.mp3')
    };
  },
  methods: {
    sendMessage() {
      if (!this.userMessage) return;
      this.messages.push({ sender: 'user', content: this.userMessage });
      this.messages.push({ sender: 'ai', content: this.getAIResponse(this.userMessage) });
      this.userMessage = '';
      this.myTrack.play();
    },
    getAIResponse(question) {
      const predefinedAnswers = {
        "hello": "Hi! I can help you with the following; shipping, return policy, Discount, payment methods, track order",
        "shipping": "shipping typically takes 3-5 business days.",
        "return policy": "You can return items within 30 days of purchase.",
        "Discount": "We currently have a 10% discount for new customers.", 
        "payment methods":"We accept Visa, Mastercard, and Paypal.", 
        "track order": "To track your order, please provide your order number."
      };
      for (let key in predefinedAnswers) {
        if (question.toLowerCase().includes(key)) {
          return predefinedAnswers[key];
          myTrack.play();
        }
      }
      return "Sorry, I'm not sure about that, please visit the Contact Us page and email your query to us.";
    }
  }
};
</script>

<style scoped>
@media (max-width: 768px) {
  .home-content h1 {
    font-size: 2em;  /* Slightly smaller heading for mobile devices */
  }

  .profile-circle {
    width: 150px;  /* Slightly smaller image circle for mobile devices */
    height: 150px;
  }

  .chatbox {
    max-width: 300px;  /* Narrower chatbox for mobile devices */
  }
}
.home-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #dda6a6;
  color: #f0f0f0;
}

.profile-circle {
  width: 200px;
  height: 200px;
  overflow: hidden;
  border-radius: 50%;
  border: 5px solid #a94949;
  box-shadow: 0 0 15px #a94949;
}

.profile-circle img {
  width: 100%;
  height: 100%;
}

.home-content {
  text-align: center;
  margin-top: 20px;
}

.home-content h1 {
  font-size: 2.5em;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px #a94949;
}


</style>




