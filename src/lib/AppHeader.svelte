<script lang="ts">
  import IconButton from "@smui/icon-button";
  import type { TopAppBarComponentDev } from "@smui/top-app-bar";
  import TopAppBar, {
    Row,
    Section,
    Title,
  } from "@smui/top-app-bar";

  import OptionsMenu from "./OptionsMenu.svelte"

  let prominent = false;
  let dense = false;
  let secondaryColor = false;
  let topAppBar: TopAppBarComponentDev;

  let lightTheme =
    typeof window === "undefined" ||
    window.matchMedia("(prefers-color-scheme: light)").matches;
  function switchTheme() {
    // window.document.body.classList.toggle('dark-mode')
    lightTheme = !lightTheme;
    let themeLink = document.head.querySelector<HTMLLinkElement>("#theme");
    if (!themeLink) {
      themeLink = document.createElement("link");
      themeLink.rel = "stylesheet";
      themeLink.id = "theme";
    }
    themeLink.href = `static/smui${lightTheme ? "" : "-dark"}.css`;
    document.head
      .querySelector<HTMLLinkElement>('link[href$="/smui-dark.css"]')
      ?.insertAdjacentElement("afterend", themeLink);
  }
</script>

<TopAppBar
  bind:this={topAppBar}
  variant="static"
  {prominent}
  {dense}
  color={secondaryColor ? "secondary" : "primary"}
>
  <Row>
    <Section>
      <Title>App Header</Title>
    </Section>
    <Section align="end" toolbar>
	  <OptionsMenu />
      {#if lightTheme}
        <IconButton
          class="material-icons"
          aria-label="Dark Mode"
          on:click={switchTheme}>dark_mode</IconButton
        >
      {/if}
      {#if !lightTheme}
        <IconButton
          class="material-icons"
          aria-label="Light Mode"
          on:click={switchTheme}>light_mode</IconButton
        >
      {/if}
    </Section>
  </Row>
</TopAppBar>

<!-- <AutoAdjust {topAppBar} style="display: flex; justify-content: space-between;">
  <div class="container"><slot /></div>
  <div class="container">
    <Button on:click={switchTheme}>
      <Label>{lightTheme ? "Lights off" : "Lights on"}</Label>
    </Button>
  </div>
</AutoAdjust> -->
