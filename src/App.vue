<template>
  <div class="home">
    <h1>Noten</h1>
  <table>
    <tr>
      <th>Fach</th>
      <th>Note</th>
      <th>Durchschnitt</th>
    </tr>
    <tr v-for="subjectsNote in subjectsNotes">
      <td>{{subjectsNote.fach}}</td>
      <td>{{subjectsNote.note}}</td> 
      <td>{{subjectsNote.note / subjectsNotes.length}}</td>
    </tr>
  </table>
      <hr>

  <div>
    <label for="fach">Fach:</label>
    <select name="fach" id="fach">
      <option v-for="subject in subjects">{{subject}}</option>
    </select> <br>
    <label for="note">Note:</label>
    <input type="number" id="note" step="0.01">
    <button @click="addSubjNote">Note hinzufügen</button>
  </div> <br> <hr>

  <label for="subject">Neuses Fach hinzufügen:</label><br>
  <input @keyup.enter="addSuject" v-model="newSubject" type="text" name="subject" id="subject">
  <button @click="addSuject">Fach hinzufügen</button>
</div>
</template>


<script>
import { ref } from 'vue';
export default {
  name: 'HomeView',

  setup: () =>{
    const newSubject = ref("")
    const newSubjectNote = ref("")
    let avg = ref("")



    const subjectsNotes = ref([{
        fach: "Englisch",
        note: 5.5
    },{
        fach: "Deutsch",
        note: 6
    },{
        fach: "Deutsch",
        note: 5
    }])
    
    const subjects = ref([
      "Englisch"
    ])

    function addSubjNote(){
      subjectsNotes.note = subjectsNotes.value.push(newSubjectNote.value);
      subjectsNotes.fach = subjects.value.push(newSubject.value);
      newSubjectNote.value = "";
    }
  
    function addSuject(){
      subjects.value.push(newSubject.value);
      newSubject.value = "";


    }
    return{
      newSubject,
      subjects,
      avg,
      addSuject,
      addSubjNote,
      subjectsNotes,
      newSubjectNote
    }
  }
}
</script>
