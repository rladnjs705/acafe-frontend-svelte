<script>
  import Router from './router.svelte';
  import { authToken, auth } from './stores';

  $: {
    if($authToken) {
      auth.createAuth();
    }
    else {
      auth.resetAuth();
    }
  }

  const initAuth = async () => {
    if($authToken) {
      await auth.createAuth();
    }
    return;
  }
</script>
<svelte:head>
	<meta name="viewport" content="width=device-width, maximum-scale=1.0, minimum-scale=1, user-scalable=yes,initial-scale=1.0" />
  <title>아카페</title>
</svelte:head>

{#await initAuth() then initAuth}
  <Router />
{/await}