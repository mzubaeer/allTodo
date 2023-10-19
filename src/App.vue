<template>
  <div class="wrapper">
    <Navbar @setSearch="searchVal = $event" />
    <NotesList :notes="filterNotes" @change="change" @delNote="delNote" />
    <AddNote @click="isModalOpen = true" />
    <Modal v-show="isModalOpen" @close="isModalOpen = false, edit = false" @addNote="addNote" :edit="edit"
      @changedNote="changedNote" :editedNote="editedNote" />
  </div>
</template>

<script>
import AddNote from './components/AddNote.vue'
import Modal from './components/Modal.vue'
import Navbar from './components/Navbar.vue'
import NotesList from './components/NotesList.vue'
export default {
  components: {
    Navbar,
    NotesList,
    AddNote,
    Modal
  },

  data() {
    return {
      isModalOpen: false,
      notes: [
        // { id: '1', title: 'audi', text: 'привет мир', date: '09.10.23' },
        // { id: '2', title: 'tecla', text: 'привет мир', date: '09.10.23' },
        // { id: '3', title: 'chevrolet', text: 'привет мир', date: '09.10.23' },
      ],
      editedNote: null,
      edit: false,
      searchVal: '',
    }
  },
  methods: {
    addNote(note) {
      this.notes = [...this.notes, note]
    },
    delNote(id) {
      this.notes = this.notes.filter((note) => note.id != id)
      // let index = this.notes.findIndex((note) => { note.id == id })
      // this.notes.splice(index, 1)
    },
    change(id) {
      this.isModalOpen = this.edit = true
      let currentNote = this.notes.find(note => note.id == id)
      this.editedNote = currentNote
    },
    changedNote(newNote) {
      this.notes.forEach((note) => {
        if (note.id == newNote.id) {
          note.title = newNote.title
          note.text = newNote.text
          note.date = newNote.date
        }
      })
    },
    getNotes() {
      let localNotes = localStorage.notes
      if (localNotes) {
        this.notes = JSON.parse(localNotes)
      }
    }
  },
  mounted() {
    this.getNotes()
  },

  computed: {
    filterNotes() {
      return this.searchVal
        ? this.notes.filter((note) => note.title.toLowerCase().includes(this.searchVal.toLowerCase())) : this.notes
    }
  },
  watch: {
    notes: {
      handler() {
        localStorage.notes = JSON.stringify(this.notes)
      },
      deep: true
    }
  }
}
</script>
