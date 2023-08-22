<template>
    <div>
      <button @click="fetchAppointments">Fetch Appointments</button>
      <div v-if="appointments">
        <!-- Display the fetched appointments here -->
        <pre>{{ appointments }}</pre>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import axios from 'axios';
  
  const appointments = ref(null);
  
  const fetchAppointments = async () => {
    const username = 'testvdit';
    const password = 'testvdit';
    const authString = btoa(`${username}:${password}`);
  
    const headers = {
      'Authorization': `Basic ${authString}`,
      'Content-Type': 'application/json'
    };
  
    const data = {
      "business_id": "20160908110055249272",
      "date": "1692705994"
    };
  
    try {
      const response = await axios.post(
        'http://beautyapi.vdit.co.uk/v1/GetAppointments',
        data,
        {
          headers,
          mode: 'no-cors' // Set mode to 'no-cors'
        }
      );
      appointments.value = response.data; // Store the fetched data
    } catch (error) {
      console.error('Error fetching appointments:', error);
    }
  };
  </script>
  