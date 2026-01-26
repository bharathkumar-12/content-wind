<script setup lang="ts">
  import { computed } from 'vue';

  const props = defineProps({
    href: {
      type: String,
      required: true,
    },
    external: {
      type: Boolean,
      default: false,
    },
    icon: {
      type: String,
      default: '',
    },
    variant: {
      type: String,
      default: 'primary',
      validator: (value: string) => ['primary', 'ghost'].includes(value),
    },
    size: {
      type: String,
      default: 'md',
      validator: (value: string) => ['sm', 'md', 'lg'].includes(value),
    },
  });

  const variantClasses = computed(
    () =>
      ({
        primary:
          'bg-slate-900 text-white dark:bg-white dark:text-slate-900 hover:bg-slate-800 dark:hover:bg-slate-100',
        ghost:
          'bg-white/80 text-slate-900 ring-1 ring-slate-200 hover:bg-white dark:bg-slate-900/70 dark:text-white dark:ring-slate-700 dark:hover:bg-slate-800',
      })[props.variant] ?? '',
  );

  const sizeClasses = computed(
    () =>
      ({
        sm: 'px-3 py-1.5 text-sm',
        md: 'px-3.5 py-2 text-sm',
        lg: 'px-4 py-2.5 text-base',
      })[props.size] ?? '',
  );

  const externalAttrs = computed(() =>
    props.external ? { target: '_blank', rel: 'noreferrer noopener' } : {},
  );
</script>

<template>
  <span class="not-prose inline-flex">
    <NuxtLink
      :to="href"
      :external="external"
      v-bind="externalAttrs"
      class="inline-flex items-center gap-2 rounded-full font-medium no-underline transition-all duration-150 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-slate-900/80 focus-visible:ring-offset-2 dark:focus-visible:ring-offset-slate-900"
      :class="[variantClasses, sizeClasses]"
      :aria-label="$slots.default ? undefined : 'Action link'"
    >
      <Icon v-if="icon" :name="icon" class="h-4 w-4" aria-hidden="true" />
      <ContentSlot :use="$slots.default" unwrap="p" />
      <Icon
        v-if="external"
        name="ph:arrow-up-right"
        class="h-4 w-4"
        aria-hidden="true"
      />
    </NuxtLink>
  </span>
</template>
