<script>
  import iconTriangle from "@iconify-icons/ic/outline-change-history";
  import iconSquare from "@iconify-icons/ic/outline-square";
  import iconCircle from "@iconify-icons/ic/outline-circle";
  import Card from "$lib/containers/Card.svelte";
  import Switch from "$lib/forms/Switch.svelte";
  import SegmentedButtonContainer from "$lib/buttons/SegmentedButtonContainer.svelte";
  import SegmentedButtonItem from "$lib/buttons/SegmentedButtonItem.svelte";
  let multiSelect = false;
</script>

<Card type="elevated">
  <h2 class="m3-font-headline-large">Segmented button</h2>
  <table>
    <tr>
      <td>
        <label for={undefined}><Switch bind:checked={multiSelect} /></label>
      </td>
      <td>{multiSelect ? "Multi-select" : "Single-select"}</td>
    </tr>
  </table>
  <div class="area">
    {#if multiSelect}
      <SegmentedButtonContainer>
        <input type="checkbox" id="segmented-a-0" />
        <SegmentedButtonItem input="segmented-a-0">$</SegmentedButtonItem>
        <input type="checkbox" id="segmented-a-1" />
        <SegmentedButtonItem input="segmented-a-1">$$</SegmentedButtonItem>
        <input type="checkbox" id="segmented-a-2" disabled />
        <SegmentedButtonItem input="segmented-a-2">$$$</SegmentedButtonItem>
      </SegmentedButtonContainer>
    {:else}
      <SegmentedButtonContainer>
        <input type="radio" name="segmented-b" id="segmented-b-0" checked />
        <SegmentedButtonItem input="segmented-b-0" icon={iconTriangle}>Tab A</SegmentedButtonItem>
        <input type="radio" name="segmented-b" id="segmented-b-1" />
        <SegmentedButtonItem input="segmented-b-1" icon={iconSquare}>Tab B</SegmentedButtonItem>
        <input type="radio" name="segmented-b" id="segmented-b-2" disabled />
        <SegmentedButtonItem input="segmented-b-2" icon={iconCircle}>Tab C</SegmentedButtonItem>
      </SegmentedButtonContainer>
    {/if}
  </div>
</Card>

<style>
  .area {
    margin: auto -1rem -1rem -1rem;
    padding: 1rem;
    border-top: solid 1px rgb(var(--m3-scheme-on-surface) / 0.12);
  }
  h2 {
    margin-top: 0;
    margin-bottom: 1rem;
  }
  label {
    display: flex;
  }
  table {
    margin-bottom: 1rem;
  }
  td + td {
    border-left: solid 0.5rem transparent;
    width: 100%;
  }
</style>
