<template >
  <div class="container">
    <div class="card">
      <h1>{{title}}</h1>
      <div class="form-control">
        <input id="input" type="text" :placeholder="placeholder" v-model="inputValue" @keypress.enter="addNote">
      </div>
      <div class="btn" @click="addNote">Добавить</div>
      <template v-if="notes.length > 0"> 
        <hr />
        <ul class="list">
          <li class="list-item" v-for="(note, index) in notes" :key=" index">
          {{note}}
          <button class="btn danger" @click="removeNote(index)">Удалить</button>
          </li>
        </ul>
        <hr />
        <p>Общее кол-во заметок: {{notes.length}}</p>
      </template>
      <p v-else >Заметок пока нет...</p>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      placeholder: 'Введите название заметки',
      title: 'Список заметок',
      inputValue: '',
      notes: []
    }
  },
  methods: {
    addNote(){
      if(this.inputValue.length > 3){
        this.notes.push(this.inputValue)

        input.style.borderColor = ''
        this.placeholder = "Введите название заметки"  

        this.inputValue = ''

        localStorage.setItem('notesArray', JSON.stringify(this.notes))
      } else {
        input.style.borderColor = 'red'
        this.placeholder = "Длина заметки должна быть больше 3 знаков"

        this.inputValue = ''
      }
    },
    removeNote(index){
      this.notes.splice(index, 1)

      localStorage.setItem('notesArray', JSON.stringify(this.notes))
    }
  },
  mounted() {
    if(localStorage.getItem('notesArray')){
      this.notes = JSON.parse(localStorage.getItem('notesArray'))
    }
  },
}
</script>

<style>
</style>
