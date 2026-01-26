<script setup lang="ts">
  import { computed, ref } from 'vue';
  import { queryContent } from '#content';

  const searchTerm = ref('');

  const {
    data: docs,
    pending,
    error,
  } = await useAsyncData('docs-search', () =>
    queryContent()
      .only(['_path', 'title', 'description', 'navigation', 'head'])
      .find(),
  );

  const results = computed(() => {
    const term = searchTerm.value.trim().toLowerCase();
    const items = docs.value || [];
    if (!term) return items.slice(0, 12);
    return items
      .map((doc) => ({
        ...doc,
        score: [
          doc.title,
          doc.description,
          doc?.head?.description,
          doc?.navigation?.title,
        ]
          .filter(Boolean)
          .join(' ')
          .toLowerCase()
          .includes(term)
          ? 1
          : 0,
      }))
      .filter((doc) => doc.score > 0);
  });
</script>

<template>
  <div class="mx-auto flex max-w-4xl flex-col gap-8 px-6 py-12 lg:px-12">
    <header class="space-y-3">
      <p class="text-sm font-medium text-slate-500 dark:text-slate-400">
        Search
      </p>
      <h1
        class="text-3xl font-semibold tracking-tight text-slate-900 dark:text-white"
      >
        Find docs fast
      </h1>
      <p class="text-slate-600 dark:text-slate-300">
        Type a keyword to filter by title or description. Clear the input to see
        recent pages.
      </p>
    </header>

    <label class="relative block">
      <span class="sr-only">Search docs</span>
      <input
        v-model="searchTerm"
        type="search"
        placeholder="Search by title, description, or topic"
        class="w-full rounded-lg border border-slate-200 bg-white px-4 py-3 text-base text-slate-900 shadow-sm outline-none ring-0 transition focus:border-slate-400 focus:ring-2 focus:ring-slate-300 dark:border-slate-700 dark:bg-slate-900 dark:text-white dark:focus:border-slate-500 dark:focus:ring-slate-700"
      />
      <Icon
        name="ph:magnifying-glass"
        class="pointer-events-none absolute right-3 top-1/2 h-5 w-5 -translate-y-1/2 text-slate-400"
        aria-hidden="true"
      />
    </label>

    <section class="min-h-[200px] space-y-4">
      <div v-if="pending" class="text-slate-500 dark:text-slate-400">
        Loading…
      </div>
      <div v-else-if="error" class="text-red-600 dark:text-red-400">
        Unable to load docs.
      </div>
      <div
        v-else-if="results.length === 0"
        class="text-slate-500 dark:text-slate-400"
      >
        No matches yet. Try a different keyword.
      </div>
      <ul v-else class="space-y-3">
        <li
          v-for="item in results"
          :key="item._path"
          class="group rounded-lg border border-slate-200 bg-white px-4 py-3 shadow-sm transition hover:-translate-y-0.5 hover:border-slate-300 hover:shadow-md dark:border-slate-800 dark:bg-slate-900 dark:hover:border-slate-700"
        >
          <NuxtLink :to="item._path" class="no-underline">
            <div class="flex items-center justify-between gap-3">
              <div class="space-y-1">
                <p class="text-sm font-semibold text-slate-900 dark:text-white">
                  {{ item.navigation?.title || item.title || item._path }}
                </p>
                <p
                  class="text-sm text-slate-600 line-clamp-2 dark:text-slate-300"
                >
                  {{
                    item.head?.description ||
                    item.description ||
                    'No description yet.'
                  }}
                </p>
              </div>
              <Icon
                name="ph:arrow-up-right"
                class="h-4 w-4 text-slate-400 transition group-hover:text-slate-600 dark:group-hover:text-slate-200"
                aria-hidden="true"
              />
            </div>
          </NuxtLink>
        </li>
      </ul>
    </section>
  </div>
</template>
