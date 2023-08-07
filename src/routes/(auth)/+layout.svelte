<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { getItem } from '$lib/utility/localStorageController';
	import { inlineSvg } from '$lib/components/utilities/utilities';

	let isAuthenticated = getItem('access_token');

	onMount(() => {
		if (isAuthenticated) {
			goto(`/trial-project`);
		}
		inlineSvg();
	});
</script>

<main>
	<slot />
</main>
