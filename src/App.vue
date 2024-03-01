<template>
  <div class="container">
    <form @submit.prevent="CardanoWarriors" class="form-container">
      <div>
        <label for="address" class="label"></label>
        <input
          type="text"
          id="address"
          v-model="formData.address"
          class="input-field"
          placeholder="Enter your wallet address or $handle..."
        />
      </div>
      <button type="submit" class="submit-button">Get my warriors!</button>
    </form>

    <div class="cards-container" v-if="posts.length > 0">
      <div v-for="post in posts" :key="post.Outpost_ID" class="card">
        <h3>{{ post.Outpost_ID }}</h3>

        <div class="info-line">
          <img :src="post.Image" class="image" alt="Warrior Image">
        </div> 
        <div class="info-line">
          <span class="label">Name:</span>
          <span class="value">{{ post["Name"] }}</span>
        </div> 
        <div class="info-line">
          <span class="label">Type:</span>
          <span class="value">{{ post["Type"] }}</span>
        </div>   
        <div class="info-line">
          <span class="label">Rarity:</span>
          <span class="value">{{ post["Rarity"] }}</span>
        </div>   
        <div class="info-line">
          <span class="label">Warrior Points:</span>
          <span class="value">{{ post["WP"] }}</span>
        </div>  

      </div>
    </div>

    <hr />
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Cardano Warriors",
  data() {
    return {
      formData: {
        address: "",
      },
      posts: [],
    };
  },
  methods: {
    async CardanoWarriors() {
      try {
        const response = await axios.post(
          "https://kadana.et.r.appspot.com/get_metadata",
          this.formData
        );
        this.posts = response.data;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

.image {
  max-width: 200px; /* Adjust the max-width as needed */
  max-height: 200px; /* Adjust the max-height as needed */
}

.container {
  box-sizing: border-box;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* padding: 20px; */
  background-image: url("https://cardanowarriors.io/assets/warriors-3b868c33.png");
  background-size: cover;
  background-position: center;
}

.loading {
  color: white;
  font-size: 24px;
  margin-top: 20px;
}

.form-container {
  width: 100%;
  max-width: 400px;
  margin-bottom: 20px;
}

.input-field {
  width: calc(100% - 24px);
  padding: 12px;
  margin-bottom: 10px;
  border: none;
  border-radius: 8px;
  background-color: rgba(255, 255, 255, 0.8);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.input-field::placeholder {
  color: #666;
}

.submit-button {
  width: calc(100% - 24px);
  padding: 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.submit-button:hover {
  background-color: #45a049;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  max-height: calc(100vh - 200px);
  overflow-y: auto;
}

.card {
  /* existing card styles */
  background-color: white; /* Add this line */
  padding: 20px;
}

.info-line {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.label {
  font-weight: bold;
  margin-right: 5px;
}

.value {
  flex-grow: 1;
}


.card h3 {
  margin-bottom: 10px;
  color: #333;
}

.card p {
  color: #666;
}

hr {
  margin-top: 20px;
  border: none;
  border-top: 1px solid #ddd;
  width: 100%;
}
</style>
