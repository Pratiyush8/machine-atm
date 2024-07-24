<script>
  import { onMount } from 'svelte';
  import { auth } from './db/firebase';
  import { onAuthStateChanged } from 'firebase/auth';
  import { Router, Link, Route } from 'svelte-routing';
  import Login from "c:/Users/Asus/app/src/routes/+page.svelte";
  import Dashboard from 'c:/Users/Asus/app/src/routes/Dashboard.svelte';

  let isAuthenticated = false;

  onMount(() => {
    onAuthStateChanged(auth, (user) => {
      isAuthenticated = !!user;
    });
  });
</script>

<Router>
  <nav>
    {#if isAuthenticated}
      <Link to="/">Dashboard</Link>
    {:else}
      <Link to="/login">Login</Link>
    {/if}
  </nav>
  <Route path="/login" component={Login} />
  <Route path="/" component={Dashboard} />
</Router>
