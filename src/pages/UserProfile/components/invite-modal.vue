<template>
  <div v-if="isVisible" class="modal-overlay" @click.self="closeModal">
    <card class="card" title="Invite New Member">
      <form @submit.prevent="sendInvite" class="form">
        <div class="row">
          <fg-input
            type="email"
            label="Email Address"
            placeholder="Enter email address"
            v-model="email"
          >
          </fg-input>
        </div>
        <div class="button-group text-center">
          <button class="update-btn" @click="sendInvite">Send Invite</button>
          <button class="close-btn" @click="closeModal">Close</button>
        </div>
      </form>
    </card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      isVisible: false,
    };
  },
  methods: {
    sendInvite() {
      if (this.email) {
        alert(`Invite sent to ${this.email}`);  // Placeholder for actual invite logic
        this.email = ''; // Clear the input after sending the invite
        this.closeModal(); // Close the modal after sending the invite
      } else {
        alert("Please enter a valid email address."); // Basic validation feedback
      }
    },
    closeModal() {
      this.isVisible = false;
      this.$emit('close'); // Emit close event to handle more actions in the parent component
    }
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.card {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  width: auto;
  max-width: 90%;
}

.button-group {
  margin-top: 20px; /* Space between input fields and buttons */
}

.update-btn, .close-btn {
  margin: 0 10px; /* Spacing between buttons */
  padding: 10px 20px; /* Larger clickable area */
  border: none;
  border-radius: 5px;
  cursor: pointer;
  color: white; /* Text color */
  font-weight: bold;
}

.update-btn {
  background-color: #4CAF50; /* Green background for update */
}

.close-btn {
  background-color: #f44336; /* Red background for close */
}
</style>
