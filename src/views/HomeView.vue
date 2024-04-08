<script setup>
import { ref } from 'vue';
import axios from 'axios';

const endpoint = ref('');
const security_key = ref('');
const payload = ref('');

const submitForm = (event) => {
  event.preventDefault();

  fetch(endpoint.value, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'security_key': security_key.value,
    'Origin': '', // Set an empty origin
  },
  body: JSON.stringify(payload.value),
})
  .then(response => response.json())
  .then(data => {
    console.log('Response:', data);
    // Handle the response data as needed
  })
  .catch(error => {
    console.error('Error:', error);
    // Handle the error as needed
  });
}


</script><template>
  <form class="request-form" @submit="submitForm">
    <div class="access-point">
      <label for="endpoint" class="input-label">Endpoint</label>
      <input type="text" v-model="endpoint" id="endpoint" class="input-field" />
      <label for="security_key" class="input-label">Security Key</label>
      <input type="text" v-model="security_key" id="security_key" class="input-field" />
    </div>

    <div class="payload">
      <textarea v-model="payload" class="payload-textarea" placeholder="Enter your payload..."></textarea>
    </div>

    <button type="submit" class="submit-button">
      Send Request
    </button>
  </form>
</template>

<style>
.request-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.access-point {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

.input-label {
  font-weight: bold;
  margin-bottom: 5px;
}

.input-field {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 700px;
}

.payload {
  margin-bottom: 20px;
}

.payload-textarea {
  width: 700px;
  height: 600px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  /* font-family: 'Courier New', Courier, monospace; */
  font-size: 14px;
  line-height: 1.5;
  overflow-y: hidden;
}

.submit-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.submit-button:hover {
  background-color: #0056b3;
}

.submit-button:focus {
  outline: none;
}
</style>