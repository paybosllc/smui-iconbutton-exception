<script lang="ts">
  import { Router, Route, Link } from "svelte-navigator";
  import HomePage from "./views/HomePage.svelte";
  import AboutPage from "./views/AboutPage.svelte";
  import SettingsPage from "./views/SettingsPage.svelte";

</script>

<Router primary={false}>
<main>
  <Route path="/">
      <HomePage />
  </Route>
  <Route path="Settings">
      <SettingsPage/>
  </Route>
  <Route path="About">
      <AboutPage />
  </Route>
</main>
</Router>
