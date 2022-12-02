<script setup>
import { ref, onMounted } from 'vue';

const studentList = ref();
const vorname = ref('');
const nachname = ref('');
const wohnort = ref('');
const geburtstag = ref(null);
const baseUrl = 'https://pb.seiwald.club/api/collections/4bhk/records';

async function createStudent() {
  const newStudent = {
    vorname: vorname.value,
    nachname: nachname.value,
    wohnort: wohnort.value,
    geburtstag: geburtstag.value,
  };
  const response = await fetch(baseUrl, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(newStudent),
  });
  getStudents();
}

async function getStudents() {
  const response = await fetch(baseUrl);
  console.log(response);
  const data = await response.json();
  console.log('data:', data.items);
  studentList.value = data.items;
}

onMounted(async () => {
  getStudents();
});
</script>

<template>
  <h1>Our Students:</h1>
  <ul>
    <li v-for="student in studentList" :key="student.id">
      {{ student.vorname }} {{ student.nachname }} wohnt in
      {{ student.wohnort }} und ist am
      {{ student.geburtstag.substring(0, 10) }} geboren.
    </li>
  </ul>

  <hr />
  <form>
    <div>
      <label for="vorname">Vorname:</label>
      <input type="text" v-model="vorname" id="vorname" />
    </div>
    <div>
      <label for="nachname">Nachname:</label>
      <input type="text" v-model="nachname" id="nachname" />
    </div>
    <div>
      <label for="wohnort">Wohnort:</label>
      <input type="text" v-model="wohnort" id="wohnort" />
    </div>
    <div>
      <label for="geburtstag">Geburtstag:</label>
      <input type="date" v-model="geburtstag" id="geburtstag" />
    </div>
    <button @click.prevent="createStudent">Create Student</button>
  </form>
</template>
