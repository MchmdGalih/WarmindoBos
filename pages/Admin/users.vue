<template>
  <section class="w-full p-3">
    <input
      type="text"
      name="search"
      id="price"
      v-model="searchUser"
      class="block rounded-md border-0 text-gray-900 ring-1 p-2 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset mb-2"
      placeholder="Search"
    />
    <div class="w-full bg-white rounded shadow-sm border">
      <h1 class="text-lg font-bold p-2">Users Management</h1>
      <div class="inline-block w-full">
        <table class="w-full text-left text-sm font-light py-2">
          <thead
            class="sticky -z-1 top-0 bg-slate-300 font-medium border-neutral-500"
          >
            <tr>
              <th scope="col" class="px-6 py-4">No.</th>
              <th scope="col" class="px-6 py-4">Nama</th>
              <th scope="col" class="px-6 py-4">Email</th>
              <th scope="col" class="px-6 py-4">Role</th>
              <th scope="col" class="px-6 py-4">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(user, index) in searchResult" :key="user.id">
              <td class="whitespace-nowrap px-6 py-4 font-medium">
                {{ index + 1 }}
              </td>
              <td class="whitespace-nowrap px-6 py-4">{{ user.name }}</td>
              <td class="whitespace-nowrap px-6 py-4">{{ user.email }}</td>
              <td class="whitespace-nowrap px-6 py-4">
                <span class="p-2 rounded bg-green-200">{{ user.role }}</span>
              </td>
              <td class="whitespace-nowrap px-6 py-4 flex items-center gap-2">
                <button class="btn btn-info">Edit</button>
                <button class="btn btn-danger">Hapus</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>
</template>

<script>
import supabase from '~/utils/supabase'
export default {
  layout: 'dashboard',
  data() {
    return {
      users: [],
      searchUser: '',
    }
  },

  computed: {
    searchResult() {
      if (this.searchUser) {
        const searchListUser = this.searchUser.toLowerCase().trim()
        return this.users.filter((user) =>
          user.name.toLowerCase().includes(searchListUser)
        )
      } else {
        return this.users
      }
    },
  },

  methods: {
    async getUser() {
      const { data } = await supabase.from('users').select()
      this.users = data
    },
  },

  mounted() {
    this.getUser()
  },
}
</script>

<style></style>
