<template>
  <aside class="bg-base-200 w-72 min-h-screen">
    <h2 class="text-lg font-bold mx-4">
      <RouterLink to="/"> Proyectos</RouterLink>
    </h2>
    <p v-if="projectsStore.noProjects" class="text-sm text-gray-500 mx-4">No hay proyectos</p>

    <!-- Menu -->
    <ul v-else class="menu bg-base-200 rounded-box w-56">
      <li v-for="project in projectsStore.projectList" :key="project.id">
        <template v-if="project.tasks.length > 0">
          <details open>
            <summary>
              <RouterLink :to="`/project/${project.id}`">
                {{ project.name }}
              </RouterLink>
            </summary>
            <ul>
              <li v-for="task in project.tasks" :key="task.id">
                <RouterLink :to="`/project/${project.id}`">{{ task.name }}</RouterLink>
              </li>
              <!-- <li>
                <details open>
                  <summary>Parent</summary>
                  <ul>
                    <li><a>Submenu 1</a></li>
                    <li><a>Submenu 2</a></li>
                  </ul>
                </details>
              </li> -->
            </ul>
          </details>
        </template>
        <template v-else>
          <RouterLink :to="`/project/${project.id}`">
            {{ project.name }}
          </RouterLink>
        </template>
      </li>
    </ul>
  </aside>
</template>

<script setup lang="ts">
import { useProjectsStore } from '../stores/projects.store';

const projectsStore = useProjectsStore();
</script>
