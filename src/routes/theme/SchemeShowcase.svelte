<script lang="ts">
  import { MaterialDynamicColors, type DynamicScheme } from "@material/material-color-utilities";
  import Icon from "@iconify/svelte";
  import iconCopy from "@iconify-icons/ic/outline-content-copy";
  import iconLight from "@iconify-icons/ic/outline-light-mode";
  import iconDark from "@iconify-icons/ic/outline-dark-mode";
  import { onMount } from "svelte";

  import type { Color, SerializedScheme } from "$lib/misc/utils";
  import StyleFromScheme from "$lib/misc/StyleFromScheme.svelte";
  import Button from "$lib/buttons/Button.svelte";
  import ColorCard from "./ColorCard.svelte";

  export let schemeLight: DynamicScheme;
  export let schemeDark: DynamicScheme;
  let showDark = false;

  const pairs = [
    ["primary", "onPrimary"],
    ["primaryContainer", "onPrimaryContainer"],
    ["secondary", "onSecondary"],
    ["secondaryContainer", "onSecondaryContainer"],
    ["tertiary", "onTertiary"],
    ["tertiaryContainer", "onTertiaryContainer"],
    ["background", "onBackground"],
    ["surface", "onSurface"],
    ["inverseSurface", "inverseOnSurface"],
    ["surfaceVariant", "onSurfaceVariant"],
    ["error", "onError"],
    ["errorContainer", "onErrorContainer"],
  ];
  const colors: Color[] = [
    "primary",
    "onPrimary",
    "primaryContainer",
    "onPrimaryContainer",
    "inversePrimary",
    "secondary",
    "onSecondary",
    "secondaryContainer",
    "onSecondaryContainer",
    "tertiary",
    "onTertiary",
    "tertiaryContainer",
    "onTertiaryContainer",
    "error",
    "onError",
    "errorContainer",
    "onErrorContainer",
    "background",
    "onBackground",
    "surface",
    "onSurface",
    "surfaceVariant",
    "onSurfaceVariant",
    "inverseSurface",
    "inverseOnSurface",
    "outline",
    "outlineVariant",
    "shadow",
    "scrim",
    "surfaceDim",
    "surfaceBright",
    "surfaceContainerLowest",
    "surfaceContainerLow",
    "surfaceContainer",
    "surfaceContainerHigh",
    "surfaceContainerHighest",
    "surfaceTint",
  ];
  const serializeScheme = (scheme: DynamicScheme) => {
    const out: Record<string, number> = {};
    for (const color of colors) {
      out[color] = MaterialDynamicColors[color as Color].getArgb(scheme);
    }
    return out as SerializedScheme;
  };
  const copyUsage = () =>
    navigator.clipboard.writeText(
      `<StyleFromScheme
  lightScheme={${JSON.stringify(serializeScheme(schemeLight))}}
  darkScheme={${JSON.stringify(serializeScheme(schemeDark))}} />`,
    );

  onMount(() => {
    showDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
  });
</script>

<StyleFromScheme
  lightScheme={serializeScheme(schemeLight)}
  darkScheme={serializeScheme(schemeDark)}
/>
<div class="content">
  <h2 class="m3-font-title-large">Your scheme 🎉</h2>
  <div class="color-container">
    {#each pairs as [bgName, fgName]}
      <ColorCard scheme={showDark ? schemeDark : schemeLight} fg={fgName} bg={bgName} />
    {/each}
  </div>
  <div class="buttons">
    <Button type="filled" iconType="left" on:click={copyUsage}>
      <Icon icon={iconCopy} />
      Copy
    </Button>
    <Button type="tonal" iconType="left" on:click={() => (showDark = !showDark)}>
      <Icon icon={showDark ? iconLight : iconDark} />
      {showDark ? "Light" : "Dark"}
    </Button>
  </div>
</div>

<style>
  .content {
    background-color: rgb(var(--m3-scheme-surface-container-low));
    padding: 1rem;
    border-radius: 1rem;
  }
  h2 {
    margin: 0 0 1rem 0;
  }
  .color-container {
    display: grid;
    border-radius: 1rem;
    overflow: hidden;
  }
  @media (min-width: 30rem) {
    .color-container {
      grid-template-columns: repeat(2, 1fr);
    }
  }
  @media (min-width: 60rem) {
    .color-container {
      grid-template-columns: repeat(4, 1fr);
    }
  }
  @media (min-width: 80rem) {
    .color-container {
      grid-template-columns: repeat(6, 1fr);
    }
  }
  .buttons {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
  }
</style>
