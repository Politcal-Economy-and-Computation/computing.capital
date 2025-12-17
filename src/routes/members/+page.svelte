<script>
  import { onMount } from 'svelte';
  
  /**
     * @type {any[] | null | undefined}
     */
  let members = $state([]);
  
  onMount(async () => {
    const response = await fetch('/data/members.json');
    members = await response.json();
  });
</script>

<div class="flex flex-col items-center">
  <h2>Members</h2>
  <ul>
    {#each members as member}
      <li>
        {member.name} • 
        <a href={member.url} target="_blank" rel="noopener noreferrer">
          {member.url}
        </a> • {member.institution}
      </li>
    {/each}
  </ul>
</div>