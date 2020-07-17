<template>
  <div id="app">
    <div class="left">
      <div class="logo">
        <a href="http://tanku.com">
						<h2>Tanku</h2>
						<span>Catatan Online</span>
					</a>
      </div>
			<div class="frame-notes">
					<button @click="newNote" class="bg-success btn btn-new-note">
						+ Catatan Baru
					</button>

					<!-- mengambil properti notes lalu ditampilkan -->
					<ListNotes :propNotes="notes" :propEditNote="editNote" />
			</div>
    </div>

    <div class="right">
				<!-- propSaveNote dibawah menjalankan fungsi pengambilan nilai ketika dipencet save 
				dari formNotes yang sudah di ambil menggunakan v-model ke notes nantinya -->
				<FormNotes :propRemoveNote="removeNote" :propSaveNote="saveNote" :propUpdateNote="updateNote" :propDataForm="dataForm" />
    </div>
  </div>
</template>

<script>
import ListNotes from './components/listNotes.vue'
import FormNotes from './components/formNotes.vue'

export default {
	name: 'app',
	data: function () {
		return {
			dataForm: {},
			// ini untuk menampilkan data di list, yang akan dilemparkan ke prop notes
			notes : [{ id:1, title: 'Tanku', description: 'Ini isi catatan' }, { id:2, title: 'Heloo', description: 'Ini adalah isi catatannya' }]
		}
	},
  components: {
		ListNotes,
		FormNotes
	},
	methods: {
		newNote(){
				this.dataForm = {id:0, title: '', description: ''}
		},
		editNote(id){
				this.dataForm = this.notes.find(note => note.id === id );
		},
		// save note ini untuk menyimpan title dan deskripsi dari form kemudian di push dan return ke notes
		saveNote(title, description){

				//fungsi dibawah untuk membuat note baru dan memberi ID pada note baru
				let newId = 0;
				
				if(this.notes.length === 0){
					newId = 1;
				} else {
					newId = this.notes[this.notes.length - 1].id + 1;
				}

				// dibawah untuk save
				let newNote = { id:newId, 'title' : title, 'description' : description }
				// dibawah fungsinya untuk push title dan description dari saveNote prop notes
				this.notes.push(newNote);
				this.editNote(newId);
		},
		updateNote(id, title, description){
			
			// ini untuk mencari index dalam array dan untuk update note
				let noteIndex = this.notes.findIndex(note => note.id === id);

				this.notes[noteIndex].title = title;
				this.notes[noteIndex].description = description;	
		},
		removeNote(id){
				let noteIndex = this.notes.findIndex(note => note.id === id);
				//splice utk membuang array
				this.notes.splice(noteIndex, 1);
		}		
	}
}
</script>

<style>
body{
     margin:0px;
     overflow:hidden;
}
#app {
     font-family: 'Avenir', Helvetica, Arial, sans-serif;
     color: #2c3e50;
     padding:0px;

     display:flex;
     width:100%;
}

.left{
     width: 400px;
     background: #f7f7f7;
     color: #616161;
}
.logo{
     padding: 25px 15px;
     border-bottom: 1px solid gainsboro;
}
.logo a{
     text-decoration:none;
}
.logo a h2{
     margin: 0px;
     display: inline;
     margin-right: 5px;
     font-size: 35px;
     text-transform: capitalize;
     color: #757575;
}
.logo a span{
     font-size: 12px;
     letter-spacing: 1px;
     text-transform: uppercase;
     color:#00d2d3;
}
.frame-notes{
     overflow-y: scroll;
     overflow-x: hidden;
     height: 85vh;
}
.bg-success{
     background: #00d2d3;
     color: white;
     outline:none;
}
.bg-success:hover{
     background:#00d2d3;
     color: white;
}
.bg-danger{
     background:#ff6b6b;
     color: white;
}
.bg-danger:hover{
     background:#ff6b6b;
}
.btn{
     border: none;
     font-size: 12px;
     text-align: center;
     letter-spacing: 1px;
     cursor: pointer;
     border-radius: 2px;
     padding: 7px 25px;
     outline:none;
}
.btn-new-note{
     width: 90%;
     padding: 12px 10px;
     margin: 10px 15px;
     text-align: left !important;
}

.right{
     width: 100%;
     overflow-y: scroll;
     height: 100vh;
     border-left: 1px solid gainsboro;
}

/* width */
::-webkit-scrollbar {
  width: 5px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f7f7f7;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
