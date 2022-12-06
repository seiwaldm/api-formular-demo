<script setup>
import { ref, onMounted } from 'vue';
import PocketBase from 'pocketbase';

const pb = new PocketBase('https://pb.seiwald.club')

const studentList = ref();
const vorname = ref('');
const nachname = ref('');
const wohnort = ref('');
const geburtstag = ref(null);


async function createStudent() {
  const record = await pb.collection('4bhk').create({
    vorname: vorname.value,
    nachname: nachname.value,
    wohnort: wohnort.value,
    geburtstag: geburtstag.value,
})
  getStudents();
}

async function getStudents() {
  const data = await pb.collection('4bhk').getFullList();
  studentList.value = data;
}

async function deleteStudent(id) {
  await pb.collection('4bhk').delete(id);
  getStudents();
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
      <button @click="deleteStudent(student.id)">X</button>
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
