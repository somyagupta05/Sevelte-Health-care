<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let currentService = null;

  let name = currentService ? currentService.name : "";
  let description = currentService ? currentService.description : "";
  let price = currentService ? currentService.price : "";

  function saveService() {
    if (!name || !description || price === "") return;

    const serviceData = {
      id: currentService ? currentService.id : Date.now(),
      name,
      description,
      price,
    };

    if (currentService) {
      dispatch("update", serviceData); // Emit update event
    } else {
      dispatch("add", serviceData); // Emit add event
    }

    // Reset form
    name = "";
    description = "";
    price = "";
  }
</script>

<form on:submit|preventDefault={saveService}>
  <input bind:value={name} placeholder="Service Name" required />
  <input bind:value={description} placeholder="Description" required />
  <input type="number" bind:value={price} placeholder="Price" required />
  <button type="submit"
    >{currentService ? "Update Service" : "Add Service"}</button
  >
</form>
