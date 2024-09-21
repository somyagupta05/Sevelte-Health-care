<script>
  import ServiceList from "./ServiceList.svelte";
  import AddService from "./AddService.svelte";

  let services = [];
  let currentService = null;

  function addService(event) {
    const newService = { id: Date.now(), ...event.detail };
    services = [...services, newService];
  }

  function updateService(event) {
    const updatedService = event.detail;
    services = services.map((service) =>
      service.id === updatedService.id ? updatedService : service
    );
    currentService = null; // Reset currentService after updating
  }

  function deleteService(id) {
    services = services.filter((service) => service.id !== id);
  }

  function editService(service) {
    currentService = service; // Set currentService for editing
  }
</script>

<AddService {currentService} on:add={addService} on:update={updateService} />
<ServiceList {services} on:delete={deleteService} on:edit={editService} />

{#if currentService}
  <AddService {currentService} on:update={updateService} />
{/if}
