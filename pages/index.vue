<script>
import ItemCard from '~/components/ItemCard.vue'

export default {
  components: { ItemCard },
  data() {
    return {
      // Daftar task
      tasks: [
        {
          id: 1,
          title: 'Task 1',
          description: 'ini deskripsi',
          isDone: false,
          category: 'Web',
        },
        {
          id: 2,
          title: 'Task 2',
          description: 'ini deskripsi 2',
          isDone: false,
          category: 'Backend',
        },
        {
          id: 3,
          title: 'Task 3',
          description: ' ini deskripsi 3',
          isDone: false,
          category: 'Frontend',
        },
      ],
      listCategory: ['Web', 'Backend', 'FrontEnd', 'Javascript', 'FullStack'],
      isCreating: false,
      isGrid: false,
      searchQuery: '',
      searchCategory: '',
      resultTask: [],
    }
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        this.searchCategory = ''
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(' ')
            .every((v) => item.title.toLowerCase().includes(v))
        })
      } else {
        return this.tasks
      }
    },

    resultCategory() {
      if (this.searchCategory.toLowerCase() === 'FullStack') {
        this.searchQuery = ''
        return this.tasks
      } else if (
        this.searchCategory &&
        this.searchCategory.toLowerCase() !== 'FullStack'
      ) {
        this.searchQuery = ''
        return this.tasks.filter(
          (item) =>
            item.category.toLowerCase() === this.searchCategory.toLowerCase()
        )
      }
    },
  },
  methods: {
    cancelFromHandler() {
      this.isCreating = !this.isCreating
    },
    submitFromHandler({ title, description, category }) {
      const newTask = {
        id: +new Date(),
        title,
        description,
        isDone: false,
        category,
      }

      this.tasks.unshift(newTask)
      this.isCreating = !this.isCreating
    },
  },
}
</script>
<template>
  <div class="container">
    <div
      class="title border-bottom d-flex align-items-center justify-content-between py-2"
    >
      <h5>Task</h5>
      <div class="d-flex align-items-center ms-auto">
        <input
          v-model="searchQuery"
          type="text"
          class="form-control me-4"
          placeholder="Search"
        />

        <select v-model="searchCategory" class="form-control">
          <option disabled value="">Search by Category</option>
          <option
            v-for="(category, i) in listCategory"
            :key="i"
            :value="category"
          >
            {{ category }}
          </option>
        </select>

        <div class="d-flex align-items-center justify-content-end w-100">
          <span class="me-2 text-center"> View As </span>
          <button
            class="btn btn-outline-secondary py-1 px-3"
            @click="isGrid = !isGrid"
          >
            {{ isGrid ? 'Grid' : 'List' }}
          </button>
        </div>
      </div>
    </div>
    <div class="list-task row">
      <div v-if="searchQuery !== ''">
        <div v-if="resultQuery.length">
          <ItemCard
            v-for="(task, i) in resultQuery"
            :key="i"
            :task="task"
            :is-grid="isGrid"
          />
        </div>
        <h3 v-else class="text-center mt-5">Catatan tidak ada</h3>
      </div>
      <div v-else-if="searchCategory !== ''">
        <div v-if="resultCategory.length">
          <ItemCard
            v-for="(task, i) in resultCategory"
            :key="i"
            :task="task"
            :is-grid="isGrid"
          />
        </div>
        <h3 v-else class="text-center mt-5">Catatan tidak ada</h3>
      </div>
      <div v-else>
        <ItemCard
          v-for="(task, i) in tasks"
          :key="i"
          :task="task"
          :is-grid="isGrid"
        />
      </div>
    </div>

    <div class="action py-2">
      <a
        v-if="!isCreating"
        href="#"
        class="add-button"
        @click="isCreating = !isCreating"
        >Add Task</a
      >
      <div v-else class="action py-2">
        <div>
          <Form
            :categories="listCategory"
            @cancel-form="cancelFromHandler"
            @submit-form="submitFromHandler"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
