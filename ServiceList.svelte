<script>
  export let services = [];
  export let onDelete;
  export let onEdit;
</script>

<ul>
  {#each services as service (service.id)}
    <li>
      <strong>{service.name}</strong>: {service.description} - ${service.price}
      <button on:click={() => onEdit(service)}>Edit</button>
      <button on:click={() => onDelete(service.id)}>Delete</button>
    </li>
  {/each}
</ul>
