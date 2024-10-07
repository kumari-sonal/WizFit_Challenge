<template>
  <div>
    <header>
      <img src="../assets/banner.png" alt="WizFit Challenge Logo" class="logo" width="100%"/>
    </header>

    <section class="what-is">
      <h2>What is WizFit Challenge?</h2>
      <button class="watch-video-btn" @click="watchVideo">Watch Video</button>
    </section>

    <section class="challenge-section">
      <img src="../assets/player.png" alt="WizFit Player" class="player-img" />
      <h3 class="challenge-title">Are you ready to take the challenge?</h3>
      <p>Download Harlem Wizards App</p>
      <div class="app-store-buttons">
        <a href="#"><img src="../assets/goolge-store.png" alt="Google Play" /></a>
        <a href="#"><img src="../assets/apple-store.png" alt="App Store" /></a>
      </div>
      <form class="campaign-form">
        <input
          type="text"
          placeholder="Search Campaign"
          class="search-input"
          v-model="searchQuery"
          @input="fetchCampaigns"
        />
        <div class="campaign-list">
          <div
            v-for="campaign in filteredCampaigns"
            :key="campaign.id"
            class="campaign"
          >
            <p>{{ campaign.school_name }}</p>
            <button class="join-btn" @click.prevent="joinCampaign(campaign)">
              Join Campaign
            </button>
          </div>
        </div>
        <p v-if="error" class="error-message">{{ error }}</p>
      </form>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '', // User input for search
      campaigns: [], // Stores the campaigns fetched from the API
      filteredCampaigns: [], // Stores filtered campaigns based on search input
      error: null // Stores error message, if any
    };
  },
  methods: {
    // Method to fetch campaigns from the API
    async fetchCampaigns() {
      try {
        const response = await fetch(
          `http://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=${this.searchQuery}`
        );
        
        if (!response.ok) {
          throw new Error('Failed to fetch campaigns');
        }

        const data = await response.json();
        console.log("data", data);
        this.campaigns = data.school_list; // Assign API response to campaigns
        this.filteredCampaigns = this.campaigns; // Initialize filtered campaigns
        this.error = null; // Reset error if successful
      } catch (error) {
        this.error = error.message; // Set error message if request fails
      }
    },
    // Method to handle video click (to be implemented)
    watchVideo() {
      alert('Watch the WizFit Challenge video!'); // Implement actual video functionality
    },
    // Method to handle joining a campaign
    joinCampaign(campaign) {
      alert(`Joined the campaign: ${campaign.name}`);
    }
  },
  created() {
    // Fetch campaigns when the component is created
    this.fetchCampaigns();
  },
  watch: {
    // Automatically fetch campaigns when the search query changes
    searchQuery() {
      this.fetchCampaigns();
    }
  }
};
</script>

<style scoped>
/* Base Styles */
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-align: center;
  background-color: #f4f4f4;
}

.header {
  background-color: #4b2a76;
  color: white;
  padding: 20px;
}
.logo {
  width: 100%; /* Responsive image width */
}

.what-is {
  margin: 20px 0;
}
.what-is h2 {
  font-size: 1.5rem;
  color: #333;
}
.watch-video-btn {
  background-color: #f34369;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.watch-video-btn:hover {
  background-color: #d12f5d;
}

.challenge-section {
  background-color: white;
  padding: 30px;
}
.player-img {
  max-width: 100%; /* Responsive image */
  height: auto;
}
.challenge-title {
  font-size: 1.5rem;
  color: #4b2a76;
  margin-top: 20px;
}
.app-store-buttons img {
  width: 150px;
  margin: 10px;
  max-width: 100%; /* Ensures buttons resize properly */
}
.campaign-form {
  margin-top: 20px;
}
.search-input {
  padding: 10px;
  width: 60%;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.campaign-list .campaign {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #f4f4f4;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
}
.join-btn {
  background-color: #4b2a76;
  color: white;
  border: none;
  padding: 5px 15px;
  cursor: pointer;
  transition: background-color 0.3s;
}
.join-btn:hover {
  background-color: #39215d;
}

.error-message {
  color: red;
  margin-top: 10px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .app-store-buttons img {
    width: 120px;
  }
  .campaign-form .search-input {
    width: 80%; /* Increase width on smaller devices */
  }
}

@media (max-width: 480px) {
  .header .main-title {
    font-size: 1.5rem;
  }
  .challenge-section .challenge-title {
    font-size: 1.2rem;
  }
  .app-store-buttons img {
    width: 100px;
  }
  .campaign-form .search-input {
    width: 90%; /* Adjust for mobile */
  }
}
</style>
