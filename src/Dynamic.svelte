<script>
	export let items;
	
	let searchQuery = '';
	
	//Does all the filtering based on the inputs in the search bar
	$: filteredList = items.filter(item => item.title.indexOf(searchQuery.toLowerCase()) !== -1);

	//Does the filtering based on the tab bar and reset filter button
	let filter = (e) =>{
		switch(e) {
  case 'public':
    return filteredList = items.filter(item => item.tags.indexOf('public') !== -1);
    break;
	case 'private':
		return filteredList = items.filter(item => item.tags.indexOf('private') !== -1);
		break;
	case 'sources':
		return filteredList = items.filter(item => item.tags.indexOf('sources') !== -1);
		break;
	case 'forks':
		return filteredList = items.filter(item => item.tags.indexOf('forks') !== -1);
		break;
  default :
    	return filteredList = items.filter(item => item.title.indexOf(searchQuery.toLowerCase()) !== -1);
		}
	}	
</script>

<b>Todo</b>
<hr />

<nav class="panel">
  <p class="panel-heading">
    Repositories
  </p>
  <div class="panel-block">
    <p class="control has-icons-left">
      <input class="input" type="text" placeholder="Search" bind:value={searchQuery}  />
      <span class="icon is-left">
        <i class="fas fa-search" aria-hidden="true"></i>
      </span>
    </p>
  </div>
	<p class="panel-tabs">
		<!-- svelte-ignore a11y-missing-attribute -->
    <a class="is-active">All</a>
		<!-- svelte-ignore a11y-missing-attribute -->
	  <a on:click|preventDefault={() => filter('public')}>{items[0].tags[0]}</a>
		<!-- svelte-ignore a11y-missing-attribute -->
		<a on:click|preventDefault={() => filter('private')}>{items[1].tags[0]}</a>
		<!-- svelte-ignore a11y-missing-attribute -->
		<a on:click|preventDefault={() => filter('sources')}>{items[0].tags[1]}</a>
		<!-- svelte-ignore a11y-missing-attribute -->
		<a on:click|preventDefault={() => filter('forks')} >{items[3].tags[1]}</a>
	</p>
	
	{#each filteredList as item}
	{#if item.icon === 'book'}
	<!-- svelte-ignore a11y-missing-attribute -->
	<a class="panel-block" >
    <span class="panel-icon">
      <i class="fas fa-book" aria-hidden="true"></i>
    </span>
    {item.title}
  </a>
	{:else}
	<!-- svelte-ignore a11y-missing-attribute -->
		<a class="panel-block" >
    <span class="panel-icon">
      <i class="fas fa-code-branch" aria-hidden="true"></i>
    </span>
    	{item.title}
  </a>
	{/if}
{/each}
	
  <div class="panel-block">
    <button class="button is-link is-outlined is-fullwidth" on:click|preventDefault={() => filter('all')}>
      Reset all filters
    </button>
  </div>
</nav>

