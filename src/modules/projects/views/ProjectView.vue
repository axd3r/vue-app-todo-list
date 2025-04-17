<template>
  <div class="w-full">
    <section class="m-2">
      <BreadCrumbs :name="project?.name ?? 'No name'" />
    </section>
    <section class="m-2">
      <div class="overflow-x-auto">
        <table class="table">
          <!-- head -->
          <thead>
            <tr>
              <th class="w-14">Completada</th>
              <th>Tarea</th>
              <th>Completada en</th>
            </tr>
          </thead>
          <tbody>
            <!-- row 2 -->
            <tr v-for="task in project?.tasks" :key="task.id" class="hover:bg-base-300">
              <th>
                <input
                  type="checkbox"
                  :checked="!!task.completedAt"
                  class="checkbox-primary"
                  @change="projectsStore.toggleTask(project?.id ?? '', task.id)"
                /><!-- (!!) doble signo de exclamacion convierte a una variable en boolean -->
              </th>
              <td>{{ task.name }}</td>
              <td>{{ task.completedAt }}</td>
            </tr>

            <tr class="hover:bg-base-300">
              <th>2</th>
              <td>
                <input
                  type="text"
                  class="input input-primary w-full opacity-60 transition-all hover:opacity-100 focus:opaity-100"
                  placeholder="Nueva Tarea"
                  v-model="newTask"
                  @keyup.enter="addTask"
                />
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import BreadCrumbs from '@/modules/common/components/BreadCrumbs.vue';
import { useProjectsStore } from '../stores/projects.store';
import { watch } from 'vue';
import { ref } from 'vue';
import type { Project } from '../interfaces/project.interface';
import { useRouter } from 'vue-router';

interface Props {
  id: string;
}

const router = useRouter();
const props = defineProps<Props>();
const projectsStore = useProjectsStore();
const project = ref<Project | null>();
const newTask = ref('');

//const project = projectsStore.projectList.find((project) => project.id === props.id);

const addTask = () => {
  if (!project.value) return;

  projectsStore.addTaskProject(project.value?.id, newTask.value);
  newTask.value = '';
};

watch(
  () => props.id,
  () => {
    project.value = projectsStore.projectList.find((project) => project.id === props.id);
    if (!project.value) {
      router.replace('/');
    }
  },
  {
    immediate: true,
  },
);
</script>

<style scoped></style>
