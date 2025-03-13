<script setup>
import { ref } from 'vue';
import { icp_workshops_backend } from 'declarations/icp_workshops_backend/index';
let translation = ref('');

async function handleSubmit(e) {
  e.preventDefault();
  const target = e.target;
  const text = target.querySelector('#text').value;
  await icp_workshops_backend.translate(text).then((response) => {
    if ("Err" in response){
      alert("BŁĄD: " + response.Err)
      
      return
    }
    
    translation.value = response.Ok;
  });
}
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />

    <h2>Tranlastor</h2>

    <form action="#" @submit="handleSubmit">
      <label for="text">Translate to german: &nbsp;</label>
      <input id="text" alt="Text" type="text" />
      <button type="submit">Translate!</button>
    </form>
    <section id="greeting">{{ translation }}</section>
  </main>
</template>
