<template>
  <div class="layout">
    <div class="left-column">
      <RequestForm @submit-request="addRequest" />
    </div>

    <div class="right-column">
      <RequestList
          :requests="requests"
          @delete-request="deleteRequest"
          @edit-request="startEdit"
      />
    </div>
  </div>

  <EditRequestWindow
      ref="editDialog"
      :data="editForm"
      @save="saveEditedRequest"
  />
</template>


<script>
import RequestForm from './components/RequestForm.vue'
import RequestList from './components/RequestList.vue'
import EditRequestWindow from "./components/EditRequestWindow.vue";

export default {
  components: {EditRequestWindow, RequestForm, RequestList },
  data() {
    return {
      requests: [],
      editIndex: null,
      editForm: null
    }
  },
  created() {
    const saved = localStorage.getItem('requests')
    if (saved) {
      this.requests = JSON.parse(saved)
    }
  },
  methods: {
    addRequest(request) {
      this.requests.push(request)
      localStorage.setItem('requests', JSON.stringify(this.requests))
    },
    deleteRequest(index) {
      this.requests.splice(index, 1)
      localStorage.setItem('requests', JSON.stringify(this.requests))
    },
    startEdit(index) {
      this.editIndex = index;
      this.editForm = { ...this.requests[index] };
      this.$refs.editDialog.show()
    },
    saveEditedRequest(updatedData) {
      this.requests.splice(this.editIndex, 1, { ...updatedData })
      localStorage.setItem('requests', JSON.stringify(this.requests))
    }
  }
}
</script>

<style scoped>
.layout{
  display: flex;
  flex-direction: row;
}

.right-column{
  margin: 25px auto;
}
</style>