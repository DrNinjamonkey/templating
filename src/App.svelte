<script lang="ts">
  import { onMount } from "svelte";
  // Reference the element with id="dash-row-template" and assign to dash variable.
  // `const` is used here because this variable will not be-reassigned again, meaning
  // it's value will not change.
  const dash = document.getElementById("dash-row-template");

  // The sample data
  const sampleApiData = [
    {
      createdDate: "2020-10-29",
      contractName: "Embedded Linux Project - Platform",
      startDate: "2020-10-12",
      total: "133 hours",
      status: "approved",
    },
    {
      createdDate: "2020-10-29",
      contractName: "Embedded Linux Project - Platform",
      startDate: "2020-10-12",
      total: "133 hours",
      status: "approved",
    },
    {
      createdDate: "2020-10-29",
      contractName: "Embedded Linux Project - Platform",
      startDate: "2020-10-12",
      total: "133 hours",
      status: "approved",
    },
    {
      createdDate: "2020-10-29",
      contractName: "Embedded Linux Project - Platform",
      startDate: "2020-10-12",
      total: "133 hours",
      status: "approved",
    },
    {
      createdDate: "2020-10-29",
      contractName: "Embedded Linux Project - Platform",
      startDate: "2020-10-12",
      total: "133 hours",
      status: "approved",
    },
  ];
  // The array of DOM elements respective to each elements in the `sampleApiData` array.
  // The array length should be the same as `sampleApiData`, Svelte will fill this array
  // because in the markup, we have defined a binding to `elements[i]`.
  const elements: HTMLDivElement[] = [];
  // The binding only happens after svelte renders the markup, which during the `onMount`
  // phase, the markup would already be rendered, so `elements` wont be an empty array anymore.
  onMount(() => {
    // Loop through the `sampleApiData` array.
    sampleApiData.forEach((sample, i) => {
      // Clone the dash element, but don't append it to the DOM yet.
      // This will essentially create an element in memory, and will not be visible yet.
      // We also prepend a `as HTMLElement` cast because the returned type `Node` does not
      // have auto-completion for `querySelector`, but because we are sure that this is an
      // HTML element, we can directly cast it for better auto-completion.
      const clone = dash.cloneNode(true) as HTMLElement;

      // Loop through key and value of each sample
      for (const [key, value] of Object.entries(sample)) {
        // Find DOM element, and replace it's text with `value`
        if (clone.querySelector("#" + key) != undefined) {
          clone.querySelector("#" + key).textContent = value.toString();
        }
      }
      // Once we're satisfied with this element that we created in memory, it's time to show it
      // to the world, so we append it to the DOM.
      elements[i].appendChild(clone);
    });
  });
</script>

{#each sampleApiData as sample, i}
  <!-- Bind this div to `elements` at index `i` -->
  <div bind:this={elements[i]} />
{/each}
