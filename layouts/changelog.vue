<template>
  <ContentDoc v-slot="{ doc }">
    <main class="mx-auto flex max-w-4xl flex-col gap-8 px-6 py-12 lg:px-12">
      <header class="space-y-3">
        <p class="text-sm font-medium text-slate-500 dark:text-slate-400">Changelog</p>
        <h1 class="text-3xl font-semibold tracking-tight text-slate-900 dark:text-white">
          {{ doc.title || 'Release notes' }}
        </h1>
        <p class="text-slate-600 dark:text-slate-300">
          {{ doc.head?.description || doc.description || 'Latest updates and fixes.' }}
        </p>
      </header>

      <article class="space-y-8">
        <ContentRenderer :value="doc" />
      </article>
    </main>
  </ContentDoc>
</template>
