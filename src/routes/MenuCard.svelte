<script lang="ts">
  import iconUndo from "@iconify-icons/ic/outline-undo";
  import iconRedo from "@iconify-icons/ic/outline-redo";
  import iconCut from "@iconify-icons/ic/outline-content-cut";
  import Card from "$lib/containers/Card.svelte";
  import Menu from "$lib/containers/Menu.svelte";
  import MenuItem from "$lib/containers/MenuItem.svelte";
  import Switch from "$lib/forms/Switch.svelte";

  let icons = false;
</script>

<Card type="elevated">
  <h2 class="m3-font-headline-large">Menu</h2>
  <table>
    <tr>
      <td>
        <label for={undefined}><Switch bind:checked={icons} /></label>
      </td>
      <td>{icons ? "Icons" : "No icons"}</td>
    </tr>
  </table>
  <div class="area">
    <Menu>
      <MenuItem icon={icons ? iconUndo : undefined}>Undo</MenuItem>
      <MenuItem icon={icons ? iconRedo : undefined} disabled>Redo</MenuItem>
      <MenuItem icon={icons ? iconCut : undefined} disabled>Cut</MenuItem>
    </Menu>
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
