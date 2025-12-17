<script>
  import { onMount } from 'svelte';

  function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
    return array;
  }
  
  /**
     * @type {any[] | null | undefined}
     */
  let members = $state([]);
  
  onMount(async () => {
    const response = await fetch('/data/members.json');
    var members_unsort = await response.json();
    members = shuffleArray(members_unsort);
  });
</script>

<div class="flex flex-col items-center">
  <h2>Members</h2>
  <ul>
    {#each members as member}
      <li>
        {member.name} • {member.institution} • 
        <a href={member.url} target="_blank" rel="noopener noreferrer">
          {member.display_url}
        </a>
      </li>
    {/each}
  </ul>
</div>