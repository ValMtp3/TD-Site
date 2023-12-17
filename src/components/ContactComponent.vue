<script setup >
import {ref} from 'vue'

const name = ref('')
const email = ref('')
const message = ref('')
const errorMessage = ref('')
const successMessage = ref('')

const submitForm = async () => {
  const webhookURL = process.env.VUE_APP_WEBHOOK_URL;
  const data = {
    content: `Nom: ${name.value}, Email: ${email.value}, Message: ${message.value}`
  }

  const response = await fetch(webhookURL, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  })

  if (response.ok) {
    name.value = ''
    email.value = ''
    message.value = ''
    successMessage.value = 'Les données ont été envoyées avec succès.'
  } else {
    errorMessage.value = 'Erreur lors de l\'envoi des données'
  }
}
</script >

<template >
  <div class="flex flex-col space-y-4 justify-center " >
      <span class="font-bold text-2xl mb-4" >Nous contacter :</span >
    <div >
      <label class="block text-sm font-medium text-gray-700" for="name" >Nom :</label >
      <input
          id="name" v-model="name" class="mt-1 block w-full shadow-sm border border-gray-700 rounded-md" type="text" >
            <span v-if="!name" class="text-red-500" >Ce champ est requis</span >
    </div >
    <div >
      <label class="block text-sm font-medium text-gray-700" for="email" >Email :</label >
      <input
          id="email" v-model="email" class="mt-1 block w-full shadow-sm border border-gray-700 rounded-md"
          type="email" >
      <span v-if="!email" class="text-red-500" >Ce champ est requis</span >
    </div >
 <div >
    <label class="block text-sm font-medium text-gray-700" for="message" >Message :</label >
    <textarea v-model="message" id="message" class="mt-1 block w-full shadow-sm border border-gray-700 rounded-md" ></textarea >
  </div >
    <button
        class="bg-black mt-3 inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white"
        type="submit" @click="submitForm" >Envoyer</button>
<div v-if="errorMessage" class="text-red-500">{{ errorMessage }}</div>
    <div v-if="successMessage" class="text-green-500">{{ successMessage }}</div>
  </div >
</template >