<script lang="ts">
  import IconButton from "@smui/icon-button";
  import Button, { Label, Icon } from "@smui/button"
  import type { TopAppBarComponentDev } from "@smui/top-app-bar";
  import TopAppBar, { Row, Section, Title } from "@smui/top-app-bar";
  import OptionsMenu from "./OptionsMenu.svelte";
  import { useNavigate } from "svelte-navigator";

  const navigate = useNavigate();

  export let headerTitle = "";
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

  function goHome() {
    navigate("/", {replace : true})
  }

  let iconButton = false

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
        <IconButton
          class="material-icons"
          aria-label="Go Back"
          on:click={goHome}>arrow_back</IconButton>
      <Button on:click$preventDefault$once={goHome}>
        <Icon class="material-icons">arrow_back</Icon>
        <Label>Back</Label>
      </Button>
      <Title>{headerTitle}</Title>
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
