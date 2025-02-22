<script lang="ts">
  import Icon from "@iconify/svelte";
  import type { IconifyIcon } from "@iconify/svelte";
  import type { HTMLAnchorAttributes, HTMLAttributes } from "svelte/elements";
  export let display = "flex";
  export let extraWrapperOptions: HTMLAttributes<HTMLDivElement> = {};
  export let extraOptions: HTMLAnchorAttributes = {};
  export let secondary = false;
  export let tab: string;
  export let items: {
    icon?: IconifyIcon;
    name: string;
    value: string;
    href: string;
  }[];
  $: tabIndex = items.findIndex((i) => i.value == tab);
</script>

<div
  class="m3-container"
  class:primary={!secondary}
  style="display: {display}; --items: {items.length}; --i: {tabIndex};"
  {...extraWrapperOptions}
>
  <div class="divider" />
  {#each items as item}
    <a href={item.href} class:tall={item.icon} class:selected={tab == item.value} {...extraOptions}>
      {#if item.icon}
        <Icon icon={item.icon} />
      {/if}
      <span class="m3-font-title-small">{item.name}</span>
    </a>
  {/each}
  <div class="bar" />
</div>

<style>
  .m3-container {
    position: relative;
    background-color: rgb(var(--m3-scheme-surface));
  }
  .divider {
    position: absolute;
    inset: auto 0 0 0;
    height: 0.0625rem;
    background-color: rgb(var(--m3-scheme-surface-container-highest));
  }
  a {
    flex: 1 0;
    height: 3rem;
    min-width: 5rem;
    white-space: nowrap;
    padding: 0 1rem;

    position: relative;
    display: flex;
    gap: 0.5rem;
    align-items: center;
    justify-content: center;

    color: rgb(var(--text));
    --text: var(--m3-scheme-on-surface-variant);
    user-select: none;
    -webkit-tap-highlight-color: transparent;
    cursor: pointer;
    transition: all 200ms;
  }
  a > :global(svg) {
    width: 1.5rem;
    height: 1.5rem;
  }

  @media (hover: hover) {
    a:hover {
      --text: var(--m3-scheme-on-surface);
      background-color: rgb(var(--text) / 0.08);
    }
  }
  a:focus-visible,
  a:active {
    --text: var(--m3-scheme-on-surface);
    background-color: rgb(var(--text) / 0.12);
  }
  a.selected {
    --text: var(--m3-scheme-on-surface);
  }

  .bar {
    position: absolute;
    background-color: rgb(var(--m3-scheme-primary));
    width: calc(100% / var(--items));
    height: 0.125rem;
    left: calc(100% / var(--items) * var(--i));
    bottom: 0;
    pointer-events: none;
    transition: all 200ms;
  }

  .primary > a {
    flex-direction: column;
    gap: 0;
  }
  .primary > a.tall {
    height: 4rem;
  }
  .primary > a > :global(svg) {
    width: 1.5rem;
    height: 1.5rem;
  }
  .primary > a.selected {
    --text: var(--m3-scheme-primary);
  }
  .primary > .bar {
    width: 3rem;
    border-radius: 0.1875rem 0.1875rem 0 0;
    margin-left: calc(50% / var(--items));
    transform: translateX(-50%);
  }

  .bar {
    print-color-adjust: exact;
    -webkit-print-color-adjust: exact;
  }
  @media screen and (forced-colors: active) {
    .bar {
      background-color: selecteditem;
    }
  }
</style>
