<script setup>
defineProps({
  profile: Object,
  repos:   Array,
})

defineEmits(['reset'])
</script>

<template>
  <div class="results-page">
    <div class="results-header">
      <button class="back-btn" @click="$emit('reset')">
        <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
          <path d="M19 12H5M12 5l-7 7 7 7"/>
        </svg>
        Back
      </button>
      <h2>Results for <span>{{ profile.login }}</span></h2>
    </div>

    <div class="profile-card">
      <img :src="profile.avatar_url" :alt="profile.login" class="avatar" />
      <div class="profile-info">
        <h3>{{ profile.name || profile.login }}</h3>
        <div class="login">@{{ profile.login }}</div>
        <p class="bio" v-if="profile.bio">{{ profile.bio }}</p>
        <div class="profile-stats">
          <div class="stat">
            <strong>{{ profile.public_repos }}</strong>
            <span>Repos</span>
          </div>
          <div class="stat">
            <strong>{{ profile.followers }}</strong>
            <span>Followers</span>
          </div>
          <div class="stat">
            <strong>{{ profile.following }}</strong>
            <span>Following</span>
          </div>
        </div>
      </div>
    </div>

    <p class="section-title">Repositories ({{ repos.length }})</p>

    <div class="repos-grid" v-if="repos.length">
      <a
        v-for="(repo, i) in repos"
        :key="repo.id"
        :href="repo.html_url"
        target="_blank"
        class="repo-card"
        :style="{ animationDelay: i * 0.05 + 's' }"
      >
        <div class="repo-name">{{ repo.name }}</div>
        <div class="repo-desc" v-if="repo.description">{{ repo.description }}</div>
        <div class="repo-meta">
          <span v-if="repo.language">
            <span class="lang-dot"></span>{{ repo.language }}
          </span>
          <span>
            <svg width="12" height="12" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
            </svg>
            {{ repo.stargazers_count }}
          </span>
          <span>
            <svg width="12" height="12" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <circle cx="12" cy="18" r="3"/><circle cx="6" cy="6" r="3"/><circle cx="18" cy="6" r="3"/>
              <path d="M18 9v1a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2V9"/>
              <line x1="12" y1="12" x2="12" y2="15"/>
            </svg>
            {{ repo.forks_count }}
          </span>
        </div>
      </a>
    </div>

    <div class="no-repos" v-else>No public repositories found.</div>
  </div>
</template>

<style scoped>
.results-page {
  flex: 1;
  padding: 2rem;
  max-width: 900px;
  margin: 0 auto;
  width: 100%;
}

.results-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2.5rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid rgba(104, 164, 241, .12);
}

.back-btn {
  background: rgba(31, 69, 145, .2);
  border: 1px solid rgba(104, 164, 241, .2);
  color: var(--cornflower);
  padding: .5rem .9rem;
  border-radius: 8px;
  cursor: pointer;
  font-family: 'Syne', sans-serif;
  font-size: .85rem;
  font-weight: 600;
  transition: background .2s, border-color .2s;
  display: flex; align-items: center; gap: .4rem;
}
.back-btn:hover { background: rgba(43, 106, 208, .25); border-color: var(--cornflower); }

.results-header h2 { font-size: 1.5rem; font-weight: 800; flex: 1; }
.results-header h2 span { color: var(--cornflower); }

.profile-card {
  background: rgba(6, 30, 71, .7);
  border: 1px solid rgba(104, 164, 241, .14);
  border-radius: 16px;
  padding: 2rem;
  display: flex;
  gap: 2rem;
  align-items: flex-start;
  margin-bottom: 2.5rem;
  backdrop-filter: blur(8px);
  animation: fadeUp .4s ease both;
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}

.avatar {
  width: 96px; height: 96px;
  border-radius: 50%;
  border: 3px solid var(--royal);
  box-shadow: 0 0 24px var(--glow);
  flex-shrink: 0;
}

.profile-info { flex: 1; min-width: 0; }
.profile-info h3 { font-size: 1.6rem; font-weight: 800; }

.login {
  font-family: 'DM Mono', monospace;
  color: var(--cornflower);
  font-size: .9rem;
  margin-top: .15rem;
}

.bio {
  margin-top: .75rem;
  color: rgba(238, 244, 255, .65);
  font-size: .9rem;
  line-height: 1.55;
}

.profile-stats {
  display: flex;
  gap: 1.5rem;
  margin-top: 1.2rem;
  flex-wrap: wrap;
}

.stat { display: flex; flex-direction: column; align-items: center; }

.stat strong {
  font-size: 1.3rem;
  font-weight: 800;
  color: var(--cornflower);
}

.stat span {
  font-size: .7rem;
  text-transform: uppercase;
  letter-spacing: .1em;
  color: rgba(238, 244, 255, .45);
  font-weight: 600;
}

.section-title {
  font-size: .7rem;
  letter-spacing: .25em;
  text-transform: uppercase;
  color: var(--royal);
  font-weight: 700;
  margin-bottom: 1rem;
}

.repos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1rem;
}

.repo-card {
  background: rgba(6, 30, 71, .5);
  border: 1px solid rgba(104, 164, 241, .1);
  border-radius: 12px;
  padding: 1.25rem;
  display: flex;
  flex-direction: column;
  gap: .6rem;
  transition: border-color .2s, transform .2s, box-shadow .2s;
  text-decoration: none;
  animation: fadeUp .4s ease both;
  backdrop-filter: blur(4px);
}

.repo-card:hover {
  border-color: rgba(104, 164, 241, .4);
  transform: translateY(-3px);
  box-shadow: 0 8px 28px rgba(43, 106, 208, .25);
}

.repo-name {
  font-weight: 700;
  color: var(--cornflower);
  font-size: .95rem;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.repo-desc {
  font-size: .8rem;
  color: rgba(238, 244, 255, .5);
  line-height: 1.5;
  flex: 1;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.repo-meta {
  display: flex;
  gap: 1rem;
  font-family: 'DM Mono', monospace;
  font-size: .75rem;
  color: rgba(238, 244, 255, .4);
}

.repo-meta span { display: flex; align-items: center; gap: .3rem; }

.lang-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--royal);
  flex-shrink: 0;
}

.no-repos {
  text-align: center;
  color: rgba(238, 244, 255, .35);
  font-size: .9rem;
  padding: 2rem;
}

@media (max-width: 600px) {
  .profile-card { flex-direction: column; }
  .profile-stats { justify-content: center; }
}
</style>
