<template>
  <dialog ref="dialog" class="edit-dialog">
    <form @submit.prevent="submit" class="edit-form">
      <h2>Редагувати заявку</h2>

      <input v-model="localData.fromCity" placeholder="Місто відправлення" required />
      <input v-model="localData.toCity" placeholder="Місто призначення" required />

      <select v-model="localData.type" required>
        <option disabled value="">Оберіть тип</option>
        <option value="gadgets">Гаджети</option>
        <option value="drinks">Напої</option>
        <option value="clothes">Одяг</option>
        <option value="medicines">Ліки</option>
        <option value="other">Інше</option>
      </select>

      <input v-model="localData.date" type="date" required />
      <textarea v-model="localData.description" placeholder="Опис" required></textarea>

      <div class="actions">
        <button type="submit" class="save">Зберегти</button>
        <button type="button" class="cancel" @click="close">Скасувати</button>
      </div>
    </form>
  </dialog>
</template>


<script>
export default {
  name: 'EditRequestWindow',
  props:{
    data:Object
  },

  data(){
    return{
      localData:{
        fromCity: '',
        toCity: '',
        type: '',
        date: '',
        description: ''
      }
    }
  },

  watch: {
    data: {
      immediate: true,
      handler(newVal) {
        if (newVal) {
          this.localData = { ...newVal }
        }
      }
    }
  },
  methods:{
    show(){
      this.$refs.dialog.showModal();
    },

    close(){
      this.$refs.dialog.close();
    },

    submit(){
      this.$emit("save", this.localData);
      this.close()
    }
  }

}
</script>

<style scoped>
.edit-dialog {
  border: none;
  border-radius: 14px;
  padding: 0;
  max-width: 450px;
  width: 90%;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.3);
  font-family: 'Segoe UI', sans-serif;
}

.edit-dialog::backdrop {
  background: rgba(0, 0, 0, 0.4);
}

.edit-form {
  background-color: #cadbda;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  border-radius: 14px;
}

.edit-form h2 {
  margin: 0;
  font-size: 20px;
  text-align: center;
  color: #333;
}

.edit-form input,
.edit-form select,
.edit-form textarea {
  padding: 10px;
  font-size: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  width: 100%;
  box-sizing: border-box;
}

.edit-form textarea {
  resize: vertical;
  min-height: 80px;
}

.actions {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin-top: 10px;
}

button {
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  font-size: 14px;
  transition: background-color 0.2s ease;
}

button.save {
  background-color: #007bff;
  color: white;
}

button.save:hover {
  background-color: #0056b3;
}

button.cancel {
  background-color: #f0f0f0;
  color: #333;
}

button.cancel:hover {
  background-color: #ddd;
}
</style>
