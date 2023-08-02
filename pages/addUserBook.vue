<template>
  <div class="container">
    <!-- Show ISBN form if isbnSearch is false -->
    <div v-if="!isbnSearch">
      <div id="isbn-form">
        <div>
          <!-- Input field for ISBN -->
          <input v-model="isbn" type="text" placeholder="ISBN du livre">
          <!-- Button to search ISBN -->
          <button @click.prevent="searchISBN">
            Rechercher
          </button>
        </div>
        <div>
          <!-- Button to skip ISBN form and add book manually -->
          <button @click.prevent="skipISBNForm">
            Le livre n'a pas d'ISBN
          </button>
        </div>
      </div>
    </div>
    <!-- Show book form if isbnSearch is true -->
    <div v-else>
      <!-- Form to add a new book -->
      <form @submit.prevent="addBook" class="book-form">
        <!-- Book details fields -->
        <label for="isbn">ISBN</label>
        <input id="isbn" type="text" :value="isbn">

        <label for="title">Titre</label>
        <input id="title" v-model="book.title" type="text">

        <label for="authors">Auteurs</label>
        <select id="authors" v-model="selectedAuthors">
          <!-- Option to add a new author -->
          <option value="addAuthor">
            Ajouter un auteur
          </option>
          <!-- Loop through existing authors -->
          <option v-for="author in authors" :key="author.id" :selected="author.id === selectedAuthorId">
            {{ author.name }}
          </option>
        </select>
        <div v-if="selectedAuthors === 'addAuthor'">
          <!-- Input fields for new author -->
          <label for="newAuthorFirstName">
            Prénom de l'auteur
          </label>
          <input id="newAuthorFirstName" v-model="newAuthor.firstName" type="text">
          <label for="newAuthorLastName">
            Nom de l'auteur
          </label>
          <input id="newAuthorLastName" v-model="newAuthor.lastName" type="text">
        </div>

        <label for="editor">
          Éditeur
        </label>
        <select id="editor" v-model="selectedEditor">
          <!-- Option to add a new editor -->
          <option value="addEditor">
            Ajouter un éditeur
          </option>
          <!-- Loop through existing editors -->
          <option v-for="editor in editors" :key="editor.id">
            {{ editor.name }}
          </option>
        </select>
        <div v-if="selectedEditor === 'addEditor'">
          <!-- Input field for new editor -->
          <label for="newEditor">
            Nouvel éditeur
          </label>
          <input id="newEditor" v-model="newEditor" type="text">
        </div>
        <label for="editor">
          Thème
        </label>
        <select id="tag" v-model="selectedTag">
          <option value="addTag">
            Ajouter un tag
          </option>
          <option v-for="tag in tags" :key="tag.id">
            {{ tag.name }}
          </option>
        </select>
        <div v-if="selectedTag === 'addTag'">
          <label for="newTag">
            Nouveau thème
          </label>
          <input id="newTag" v-model="newTag" type="text">
        </div>

        <label for="publicationDate">
          Date de parution
        </label>
        <input id="publicationDate" v-model="book.publicationDate" type="date">

        <label for="coverType">
          Type de couverture
        </label>
        <select id="coverType" v-model="selectedCoverType">
          <option value="addCoverType">
            Ajouter un type de couverture
          </option>
          <option v-for="coverType in coverTypes" :key="coverType.id">
            {{ coverType.name }}
          </option>
        </select>
        <div v-if="selectedCoverType === 'addCoverType'">
          <label for="newCoverType">
            Nouveau type de couverture
          </label>
          <input id="newCoverType" v-model="newCoverType" type="text">
        </div>

        <label for="paperType">
          Type de papier
        </label>
        <select id="paperType" v-model="selectedPaperType">
          <option value="addPaperType">
            Ajouter un type de papier
          </option>
          <option v-for="paperType in paperTypes" :key="paperType.id">
            {{ paperType.name }}
          </option>
        </select>
        <div v-if="selectedPaperType === 'addPaperType'">
          <label for="newPaperType">
            Nouveau type de papier
          </label>
          <input id="newPaperType" v-model="newPaperType" type="text">
        </div>

        <label for="format">
          Format du papier
        </label>
        <select id="format" v-model="selectedFormat">
          <option value="addFormat">
            Ajouter un format
          </option>
          <option v-for="format in formats" :key="format.id">
            {{ format.name }}
          </option>
        </select>
        <div v-if="selectedFormat === 'addFormat'">
          <label for="newFormat">
            Nouveau type de papier
          </label>
          <input id="newFormat" v-model="newFormat" type="text">
        </div>

        <label for="conservationState">
          État de conservation
        </label>
        <select id="conservationState" v-model="selectedConservationState">
          <option v-for="conservationState in conservationStates" :key="conservationState.id">
            {{ conservationState.name }}
          </option>
        </select>

        <label for="status">
          Statut de la vente
        </label>
        <select id="status" v-model="selectedStatus">
          <option v-for="status in statuses" :key="status.id">
            {{ status.name }}
          </option>
        </select>

        <label for="comments">
          Commentaire
        </label>
        <textarea id="comments" v-model="book.comments"></textarea>
        <div class="prices">
          <div>
            <div class="row">
              <label for="purchasePrice">
                Prix d'achat :
              </label>
              <input id="purchasePrice" v-model="book.purchasePrice" type="number">
            </div>
            <div class="column">
              <label for="purchaseDate">
                Date d'achat
              </label>
              <input id="purchaseDate" v-model="book.purchaseDate" type="date">
            </div>
          </div>
          <div>
            <div class="row">
              <label for="sellingPrice">
                Prix de vente
              </label>
              <input id="sellingPrice" v-model="book.sellingPrice" type="number">
            </div>
            <div class="column">
              <label for="isOnEbay">
                Avez-vous mis ce livre en vente sur eBay ?
              </label>
              <input id="isOnEbay" v-model="book.isOnEbay" type="checkbox">
            </div>

            <div v-if="book.isOnEbay" class="ebay-fields">
              <div>
                <label for="onSaleDate">
                  Date de mise en vente
                </label>
                <input id="onSaleDate" v-model="book.onSaleDate" type="date">
              </div>
              <div>
                <label for="ebayLink">
                  Lien eBay
                </label>
                <input id="ebayLink" v-model="book.ebayLink" type="text">
              </div>
            </div>
          </div>
        </div>

        <button type="submit">
          Ajouter le livre
        </button>
      </form>
    </div>
    <ModalMsg
      v-if="isModalMsgOpen"
      title="Votre livre a bien été ajouté !"
      content="Votre livre a été ajouté, vous allez être redirigé vers votre bibliothèque."
      buttonMsg="Fermer"
      @close="closeModalMsg"
    />
  </div>
</template>

<script>
import axios from 'axios'
import { mapGetters } from 'vuex'
import ModalMsg from '@/components/ModalMsg'

export default {
  name: 'AddBook',
  components: {
    ModalMsg
  },
  data () {
    return {
      isModalMsgOpen: false,
      token: null,
      isbn: '',
      isbnFound: false,
      isbnSearch: false,
      booktoAdd: { },
      userbooktoAdd: { },
      selectedAuthorId: 0,
      book: {
        isbn: '',
        title: '',
        authors: [],
        publicationDate: '',
        comments: '',
        purchasePrice: 0,
        sellingPrice: 0,
        isOnEbay: false,
        onSaleDate: '',
        ebayLink: ''
      },
      authors: [],
      selectedAuthors: '',
      newAuthor: {
        firstName: '',
        lastName: ''
      },
      editors: [],
      selectedEditor: '',
      newEditor: '',
      tags: [],
      selectedTag: '',
      newTag: '',
      coverTypes: [],
      selectedCoverType: '',
      newCoverType: '',
      paperTypes: [],
      selectedPaperType: '',
      newPaperType: '',
      formats: [],
      selectedFormat: '',
      newFormat: '',
      conservationStates: [],
      selectedConservationState: '',
      newConservationState: '',
      statuses: [],
      selectedStatus: '',
      newStatus: ''
    }
  },
  mounted () {
    this.getAllAuthors()
    this.getAllCoverTypes()
    this.getAllPaperTypes()
    this.getAllFormats()
    this.getAllEditors()
    this.getAllConservationStates()
    this.getAllStatuses()
    this.getAllTags()
  },
  methods: {
    ...mapGetters('auth', ['getToken']),
    openModalMsg () {
      this.isModalMsgOpen = true
    },
    closeModalMsg () {
      this.isModalMsgOpen = false
    },
    async searchISBN () {
      try {
        this.token = this.getToken()
        const response = await axios.get(`http://localhost:8000/api/auth/isbn_codes/search/${this.isbn}`, {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        if (response.data.message === 'Book found') {
          this.isbnSearch = true
          this.isbnFound = true
          this.book.title = response.data.book.title
          this.book.publicationDate = response.data.book.publication_date
          this.selectedAuthorId = response.data.book.book_authors[0].id
        } else {
          this.isbnSeach = true
          this.skipISBNForm()
        }
      } catch (error) {
        console.error(error)
      }
    },
    async addBook () {
      try {
        this.token = this.getToken()
        // if (!this.isbnFound) {
        if (this.selectedAuthors === 'addAuthor') {
          const newAuthorData = {
            firstname: this.newAuthor.firstName,
            lastname: this.newAuthor.lastName
          }
          const response = await axios.post('http://localhost:8000/api/auth/authors', newAuthorData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.authors = response.data.data.id
        } else {
          const authors = this.selectedAuthors.split(' ')

          const author = await axios.get(`http://localhost:8000/api/authors/${authors[0]}/${authors[1]}`, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.authors = author.data[0].id
        }
        if (this.selectedTag === 'addTag') {
          const newTagData = {
            tag_name: this.newTag
          }
          const response = await axios.post('http://localhost:8000/api/auth/tags', newTagData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.tag = response.data.tag.id
        } else {
          const tag = await axios.get(`http://localhost:8000/api/tags/show/${this.selectedTag}`, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.tag = tag.data.id
        }
        if (this.selectedCoverType === 'addCoverType') {
          const newCoverTypeData = {
            book_cover_name: this.newCoverType
          }
          const response = await axios.post('http://localhost:8000/api/auth/book_covers', newCoverTypeData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.book_cover = response.data.book_cover.id
        } else {
          const bookcover = await axios.get(`http://localhost:8000/api/book_covers/show/${this.selectedCoverType}`, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.book_cover = bookcover.data.id
        }
        if (this.selectedPaperType === 'addPaperType') {
          const newPaperTypeData = {
            paper_type_name: this.newPaperType
          }
          const response = await axios.post('http://localhost:8000/api/auth/paper_types', newPaperTypeData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.book_cover = response.data.data.id
        } else {
          const papertype = await axios.get(`http://localhost:8000/api/paper_types/show/${this.selectedPaperType}`, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.paper_type = papertype.data.id
        }
        if (this.selectedFormat === 'addFormat') {
          const newFormatData = {
            format_name: this.newFormat
          }
          const response = await axios.post('http://localhost:8000/api/auth/formats', newFormatData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.format = response.data.format.id
        } else {
          const format = await axios.get(`http://localhost:8000/api/formats/show/${this.selectedFormat}`, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.format = format.data.id
        }

        if (this.selectedEditor === 'addEditor') {
          const newEditorData = {
            editor_name: this.newEditor
          }
          const response = await axios.post('http://localhost:8000/api/auth/editors', newEditorData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.editor = response.data.data.id
        } else {
          const editor = await axios.get(`http://localhost:8000/api/editors/show/${this.selectedEditor}`, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.editor = editor.data.id
        }
        const isbn = await axios.get(`http://localhost:8000/api/isbn_codes/show/${this.isbn}`, {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        if (isbn.data === '') {
          const newIsbnData = {
            code: this.isbn,
            validated: 0
          }
          const response = await axios.post('http://localhost:8000/api/auth/isbn_codes', newIsbnData, {
            headers: {
              Authorization: `Bearer ${this.token}`
            }
          })
          this.booktoAdd.isbn = response.data.data.id
        } else {
          this.booktoAdd.isbn = isbn.data.id
        }
        this.booktoAdd.title = this.book.title.trim()
        this.booktoAdd.publicationDate = this.book.publicationDate.trim()
        this.booktoAdd.validated = 0
        const book = {
          title: this.booktoAdd.title,
          parution_date: this.booktoAdd.publicationDate,
          validated: this.booktoAdd.validated,
          book_cover_id: this.booktoAdd.book_cover,
          paper_type_id: this.booktoAdd.paper_type,
          format_id: this.booktoAdd.format,
          isbn_code_id: this.booktoAdd.isbn,
          editor_id: 1,
          tags: [
            this.booktoAdd.tag
          ],
          authors: [
            this.booktoAdd.authors
          ]
        }
        const bookResponse = await axios.post('http://localhost:8000/api/auth/books', book, {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })

        // Userbook

        this.userbooktoAdd.book_id = bookResponse.data.data.id

        if (this.book.isOnEbay) {
          this.userbooktoAdd.on_ebay = true
          this.userbooktoAdd.ebay_link = this.book.ebayLink
          this.userbooktoAdd.on_sale_date = this.book.onSaleDate.trim()
          this.sold_date = null
        } else {
          this.userbooktoAdd.on_ebay = false
          this.userbooktoAdd.ebay_link = ''
          this.userbooktoAdd.on_sale_date = ''
          this.sold_date = null
        }

        this.userbooktoAdd.comments = this.book.comments.trim()
        this.userbooktoAdd.purchase_price = this.book.purchasePrice.trim()
        this.userbooktoAdd.purchase_date = this.book.purchaseDate.trim()
        this.userbooktoAdd.selling_price = this.book.sellingPrice.trim()

        const response = await axios.get(`http://localhost:8000/api/conservation_states/show/${this.selectedConservationState}`, {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        this.userbooktoAdd.conservation_state_id = response.data.id
        const responseStatus = await axios.get(`http://localhost:8000/api/statuses/show/${this.selectedStatus}`, {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        this.userbooktoAdd.status_id = responseStatus.data.id
        const userbook = {
          book_id: this.userbooktoAdd.book_id,
          comments: this.userbooktoAdd.comments,
          purchase_price: this.userbooktoAdd.purchase_price,
          selling_price: this.userbooktoAdd.selling_price,
          purchase_date: this.userbooktoAdd.purchase_date,
          on_sale_date: this.userbooktoAdd.on_sale_date,
          sold_date: this.userbooktoAdd.sold_date,
          conservation_state_id: this.userbooktoAdd.conservation_state_id,
          status_id: this.userbooktoAdd.status_id
        }
        await axios.post('http://localhost:8000/api/auth/user_books', userbook, {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        })
        this.openModalMsg()
        this.$router.push('/perso')
        // } else {
        //   console.log('userbookResponse')
        // }
      } catch (error) {
        console.error(error)
      }
    },
    skipISBNForm () {
      this.isbnSearch = true
      this.isbnFound = false
    },
    async getAllAuthors () {
      const response = await axios.get('http://localhost:8000/api/authors', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.data.length; i++) {
        this.authors.push({ id: response.data.data[i].id, name: response.data.data[i].firstname + ' ' + response.data.data[i].lastname })
      }
    },
    async getAllCoverTypes () {
      const response = await axios.get('http://localhost:8000/api/book_covers', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.book_covers.length; i++) {
        this.coverTypes.push({ id: response.data.book_covers[i].id, name: response.data.book_covers[i].book_cover_name })
      }
    },
    async getAllPaperTypes () {
      const response = await axios.get('http://localhost:8000/api/paper_types', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.data.length; i++) {
        this.paperTypes.push({ id: response.data.data[i].id, name: response.data.data[i].paper_type_name })
      }
    },
    async getAllFormats () {
      const response = await axios.get('http://localhost:8000/api/formats', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.formats.length; i++) {
        this.formats.push({ id: response.data.formats[i].id, name: response.data.formats[i].format_name })
      }
    },
    async getAllEditors () {
      const response = await axios.get('http://localhost:8000/api/editors', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.data.length; i++) {
        this.editors.push({ id: response.data.data[i].id, name: response.data.data[i].editor_name })
      }
    },
    async getAllConservationStates () {
      const response = await axios.get('http://localhost:8000/api/conservation_states', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.data.length; i++) {
        this.conservationStates.push({ id: response.data.data[i].id, name: response.data.data[i].state_name })
      }
    },
    async getAllStatuses () {
      const response = await axios.get('http://localhost:8000/api/statuses', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.data.length; i++) {
        this.statuses.push({ id: response.data.data[i].id, name: response.data.data[i].name })
      }
    },
    async getAllTags () {
      const response = await axios.get('http://localhost:8000/api/tags', {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      })
      for (let i = 0; i < response.data.tags.length; i++) {
        this.tags.push({ id: response.data.tags[i].id, name: response.data.tags[i].tag_name })
      }
    }
  }
}
</script>

<style scoped>
/* CSS pour le premier formulaire */
#isbn-form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-bottom: 16px;
}
#isbn-form div {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-bottom: 16px;
}
#isbn-form input[type="text"] {
  border: 1px solid #444;
  width: 70%;
  margin-right: 5px;
}

#isbn-form button {
  color: white;
  background-color: #6C1B39;
  border: none;
  padding: 8px;
}

#isbn-form button:focus {
  outline: none;
}

/* CSS pour le deuxième formulaire */
.book-form {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 16px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  margin: 0 auto;
}

.book-form label {
  margin-bottom: 8px;
}

.book-form input[type="text"],
.book-form input[type="date"],
.book-form textarea,
.book-form select {
  border: 1px solid #444;
  padding: 8px;
  margin-bottom: 16px;
}

.book-form select {
  width: 100%;
}

.book-form textarea {
  height: 100px;
}

.book-form button {
  margin-top: 16px;
  background-color: #6C1B39;
  color: white;
  border: none;
  padding: 8px 16px;
  cursor: pointer;
}

.book-form button:focus {
  outline: none;
}

.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}
.column {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}
</style>
