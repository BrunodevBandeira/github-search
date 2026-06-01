<script setup>
import { ref } from 'vue'
import SearchPage from './components/SearchPage.vue'
import ResultsPage from './components/ResultsPage.vue'

const query   = ref('')
const loading = ref(false)
const error   = ref('')
const profile = ref(null)
const repos   = ref([])

async function search() {
  const user = query.value.trim()
  if (!user) return
  loading.value = true
  error.value   = ''
  profile.value = null
  repos.value   = []

  try {
    const [uRes, rRes] = await Promise.all([
      fetch(`https://api.github.com/users/${user}`),
      fetch(`https://api.github.com/users/${user}/repos?per_page=30&sort=stars`),
    ])
    if (!uRes.ok) throw new Error(uRes.status === 404 ? 'User not found.' : 'GitHub API error.')
    profile.value = await uRes.json()
    repos.value   = rRes.ok ? await rRes.json() : []
  } catch (e) {
    error.value = e.message
  } finally {
    loading.value = false
  }
}

function reset() {
  profile.value = null
  repos.value   = []
  error.value   = ''
}
</script>

<template>
  <SearchPage
    v-if="!profile"
    v-model:query="query"
    :loading="loading"
    :error="error"
    @search="search"
  />
  <ResultsPage
    v-else
    :profile="profile"
    :repos="repos"
    @reset="reset"
  />
</template>
