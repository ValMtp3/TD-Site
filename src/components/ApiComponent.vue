<script setup >
import {ref} from 'vue'

const name = ref('')
const email = ref('')
const parametre = ref('')
const result = ref('')

const submitForm = async () => {
  const response = await fetch(name.value + parametre.value, {
    method: email.value,
    headers: {
      'Content-Type': 'application/json'
    },
  })

  if (response.ok) {
    const data = await response.json()
    result.value = data;
    console.log("ok")
  } else {
    result.value = 'Error: ' + response.status
    console.log("FAIL")
  }
}
</script >

<template >
  <div class="flex flex-col space-y-4 justify-center " >
      <span class="font-bold text-2xl mb-4" >Contacter une API GET :</span >
    <div >
      <label class="block text-sm font-medium text-gray-700" for="name" >URL :</label >
    <input id="url" v-model="name" class="mt-1 block w-full shadow-sm border border-gray-700 rounded-md" type="text" >
            <span v-if="!name" class="text-red-500" >Ce champ est requis</span >
    </div >
    <div >
      <label class="block text-sm font-medium text-gray-700" for="email" >Méthode :</label >
    <input id="methode" v-model="email" class="mt-1 block w-full shadow-sm border border-gray-700 rounded-md" type="text" >
      <span v-if="!email" class="text-red-500" >Ce champ est requis</span >
    </div >
 <div >
    <label class="block text-sm font-medium text-gray-700" for="parametre" >Paramètres :</label >
    <input id="parametre" v-model="parametre" class="mt-1 block w-full shadow-sm border border-gray-700 rounded-md" type="text" >
            <span v-if="!parametre" class="text-red-500" >Ce champ est requis</span >
  </div >
    <button
        class="bg-black mt-3 inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white"
        type="submit" @click="submitForm" >Transmettre</button >
    <div>
    <span class="font-bold text-2xl mb-4 mx-4" >Résultat :</span >
    <pre>
      {{ result }}
    </pre>
  </div>
  </div >

</template >