<script setup>
defineProps({
  query:   String,
  loading: Boolean,
  error:   String,
})

const emit = defineEmits(['update:query', 'search'])
</script>

<template>
  <div class="search-page">
    <div class="brand">
      <div class="brand-icon">
        <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
          <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
        </svg>
      </div>
      <h1>Git<span>Hub</span></h1>
      <p>User Search</p>
    </div>

    <div class="search-box">
      <div class="input-wrap">
        <span class="input-icon">
          <svg width="18" height="18" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
          </svg>
        </span>
        <input
          :value="query"
          type="text"
          placeholder="Enter GitHub username..."
          :disabled="loading"
          @input="emit('update:query', $event.target.value)"
          @keyup.enter="emit('search')"
        />
      </div>

      <button
        class="btn-search"
        :disabled="loading || !query.trim()"
        @click="emit('search')"
      >
        <div class="spinner" v-if="loading"></div>
        <svg v-else width="16" height="16" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
          <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
        </svg>
        {{ loading ? 'Searching…' : 'Search' }}
      </button>

      <div class="error-msg" v-if="error">{{ error }}</div>
    </div>
  </div>
</template>

<style scoped>
.search-page {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  gap: 2.5rem;
}

.brand { text-align: center; }

.brand-icon {
  width: 80px; height: 80px;
  background: linear-gradient(135deg, var(--navy), var(--royal));
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  margin: 0 auto 1.25rem;
  box-shadow: 0 0 40px var(--glow);
  animation: pulse 3s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { box-shadow: 0 0 40px var(--glow); }
  50%       { box-shadow: 0 0 70px rgba(43, 106, 208, .6); }
}

.brand-icon svg { width: 44px; height: 44px; fill: var(--white); }

.brand h1 {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 800;
  letter-spacing: -2px;
  line-height: 1;
}

.brand h1 span { color: var(--cornflower); }

.brand p {
  margin-top: .5rem;
  font-size: .85rem;
  letter-spacing: .3em;
  text-transform: uppercase;
  color: var(--royal);
  font-weight: 600;
}

.search-box {
  width: 100%;
  max-width: 520px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.input-wrap { position: relative; }

.input-wrap input {
  width: 100%;
  padding: 1rem 1.25rem 1rem 3.25rem;
  background: rgba(31, 69, 145, .18);
  border: 1.5px solid rgba(104, 164, 241, .22);
  border-radius: 10px;
  color: var(--white);
  font-family: 'DM Mono', monospace;
  font-size: 1rem;
  outline: none;
  transition: border .25s, box-shadow .25s, background .25s;
}

.input-wrap input::placeholder { color: rgba(104, 164, 241, .45); }

.input-wrap input:focus {
  border-color: var(--cornflower);
  background: rgba(31, 69, 145, .28);
  box-shadow: 0 0 0 4px rgba(104, 164, 241, .12);
}

.input-icon {
  position: absolute;
  left: 1rem; top: 50%;
  transform: translateY(-50%);
  color: var(--royal);
  display: flex;
}

.btn-search {
  width: 100%;
  padding: 1rem;
  background: linear-gradient(135deg, var(--navy) 0%, var(--royal) 100%);
  border: none;
  border-radius: 10px;
  color: var(--white);
  font-family: 'Syne', sans-serif;
  font-size: 1rem;
  font-weight: 700;
  letter-spacing: .08em;
  cursor: pointer;
  display: flex; align-items: center; justify-content: center; gap: .6rem;
  transition: transform .15s, box-shadow .2s, background .2s;
  box-shadow: 0 4px 24px rgba(43, 106, 208, .4);
}

.btn-search:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 8px 32px rgba(43, 106, 208, .55);
  background: linear-gradient(135deg, var(--royal) 0%, var(--cornflower) 100%);
}

.btn-search:active:not(:disabled) { transform: translateY(0); }
.btn-search:disabled { opacity: .6; cursor: not-allowed; }

.spinner {
  width: 18px; height: 18px;
  border: 2.5px solid rgba(255, 255, 255, .3);
  border-top-color: #fff;
  border-radius: 50%;
  animation: spin .7s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }

.error-msg {
  text-align: center;
  color: #f87171;
  font-family: 'DM Mono', monospace;
  font-size: .85rem;
  padding: .75rem 1.25rem;
  background: rgba(248, 113, 113, .08);
  border: 1px solid rgba(248, 113, 113, .25);
  border-radius: 8px;
}
</style>
