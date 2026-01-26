<!-- Render raw Markdown examples with consistent spacing and keyboard-friendly scrolling. -->
<template>
  <figure class="not-prose my-6">
    <pre
      class="max-w-full overflow-x-auto rounded-lg border border-slate-200 bg-slate-50 px-4 py-3 font-mono text-sm text-slate-800 shadow-sm dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
      aria-label="Markdown example"
      tabindex="0"
    >
      <ContentSlot :use="$slots.default" unwrap="p" />
    </pre>
  </figure>
</template>
