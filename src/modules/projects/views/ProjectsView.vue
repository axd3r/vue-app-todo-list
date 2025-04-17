<template>
  <div class="overflow-x-auto w-full">
    <table class="table">
      <!-- head -->
      <thead>
        <tr>
          <th></th>
          <th>Proyecto</th>
          <th>Tareas</th>
          <th>Avance</th>
        </tr>
      </thead>
      <tbody>
        <!-- row 1 -->
        <tr
          v-for="(project, index) in projectsStore.projectsWithCompletion"
          class="hover:bg-base-300"
          :key="project.id"
        >
          <th>{{ index + 1 }}</th>
          <td>{{ project.name }}</td>
          <td>{{ project.taskCount }}</td>
          <td>
            <progress
              class="progress progress-primary w-56"
              :value="project.completion"
              max="100"
            ></progress>
            {{ project.completion }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <InputModal
    :open="modalOpen"
    @close="modalOpen = false"
    placeholder="Ingrese el nombre del proyecto"
    @value="projectsStore.addProject"
    title="Nuevo Proyecto"
    sub-title="Dale un nombre unico a tu proyecto"
  />

  <CustomModal :open="customModalOpen">
    <template #header> <h1 class="text-3xl">Titulo del modal</h1></template>
    <template #body>
      <p>HOL HOL HOLA</p>
    </template>
    <template #actions>
      <div class="flex justify-end">
        <button @click="customModalOpen = false" class="btn mr-4">Close</button>
        <button @click="customModalOpen = false" class="btn btn-primary">Aceptar</button>
      </div>
    </template>
  </CustomModal>

  <FabButton @click="modalOpen = true">
    <AddCircle />
  </FabButton>

  <FabButton @click="customModalOpen = true" position="bottom-left">
    <ModalIcon />
  </FabButton>
</template>

<script setup lang="ts">
import FabButton from '@/modules/common/components/FabButton.vue';
import AddCircle from '@/modules/common/icons/AddCircle.vue';
import InputModal from '../../common/components/InputModal.vue';
import CustomModal from '@/modules/common/components/CustomModal.vue';
import ModalIcon from '@/modules/common/icons/ModalIcon.vue';
import { ref } from 'vue';
import { useProjectsStore } from '../stores/projects.store';

const modalOpen = ref(false);
const customModalOpen = ref(false);

const projectsStore = useProjectsStore();

//en project.store se crea la funcion que traera un nuevo dato a la tabla
/* const onNewValue = (projectName: string) => {
  projectsStore.projectList.push({
    id: '3',
    name: projectName,
    tasks: []
  })
}; */
</script>
