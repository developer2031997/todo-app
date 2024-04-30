<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-white margin-top">
      <q-input bottom-slots class="col" square filled bg-color="white" v-model="newTask" label="Add Task"
        @key.enter="addNewTask" dense>
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addNewTask" />
        </template>
      </q-input>
    </div>
    <p class="task-heading"> All Task List :</p>
    <hr />
    <q-list class="bg-white" separator bordered>
      <q-item tag="label" v-for="task in todoData" :key="task.id" clickable @click="toggleTaskStatus(task)"
        :class="{ 'Done bg-blue-1': task.isDone }" v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="task.isDone" :color="color" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.isDone" side>
          <q-btn flat round dense color="primary" icon="delete" @click="confirmDelete(task)" />
        </q-item-section>
      </q-item>
    </q-list>

    <div v-if="!todoData.length" class="no-task absolute-center d-flex">
      <q-icon name="check" size="100px" color="primary" />
      <p class="text-h5 text-primary text-center">No task</p>
    </div>
  </q-page>

</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

defineOptions({
  name: 'TodoPage'
});

const color = ref('primary');

const newTask = ref('')

const todoData = ref([]);

const $q = useQuasar()


const addNewTask = () => {
  const id = todoData.value.length > 0 ? Math.max(...todoData.value.map(task => task.id)) + 1 : 1;

  todoData.value.push({
    id: id,
    title: newTask.value,
    isDone: false
  });

  (() => {
    $q.notify({
      message: 'task Added sucessfully !!!',
      color: 'purple',
    })
  })();

  newTask.value = '';
}

const toggleTaskStatus = (task) => {
  task.isDone = !task.isDone;
};

// const deleteTask = (id) => {
//   return todoData.value = todoData.value.filter((item) => item.id !== id);
// }

const confirmDelete = (task) => {
  const confirmed = window.confirm(`Are you sure you want to delete the task "${task.title}"?`);
  if (confirmed) {
    deleteTask(task.id);

    (() => {
      $q.notify({
        message: 'task Deleted sucessfully !!!',
        color: 'purple',
      })
    })();
  }
};

const deleteTask = (id) => {
  todoData.value = todoData.value.filter((item) => item.id !== id);

}



</script>

<style>
.Done {
  text-decoration: line-through;
}

.margin-top {
  margin: 0px;
  margin-top: 15px;
  border-bottom: 1px solid #000;
}

.task-heading {
  padding: 10px 30px;
  margin: 0px;
  margin-top: 15px;
  font-weight: 800;

}
</style>
