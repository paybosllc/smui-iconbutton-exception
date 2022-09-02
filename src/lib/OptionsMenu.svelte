<script lang="ts">
  import Button, { Label } from "@smui/button";
  import Menu from "@smui/menu";
  import type { MenuComponentDev } from "@smui/menu";
  import List, { Item, Separator, Text } from "@smui/list";
  import { useNavigate, useLocation } from "svelte-navigator";

  const navigate = useNavigate();
  const location = useNavigate();
  let menu: MenuComponentDev;
  let clicked = "nothing yet";

$: console.log(location)
</script>

<div>
  <Button on:click={() => menu.setOpen(true)}>
    <Label>...</Label>
  </Button>
  <Menu bind:this={menu}>
    <List>
      <Item on:SMUI:action={() => (clicked = "Option One")}>
        <Text>Option One</Text>
      </Item>
      <Item on:SMUI:action={() => (clicked = "Option Two")}>
        <Text>Option Two</Text>
      </Item>
      <Item on:SMUI:action={() => { navigate('/Settings', { replace: true})}}>
        <Text>Settings</Text>
      </Item>
      <Separator />
      <Item on:SMUI:action={() => navigate('/About')}>
        <Text>About</Text>
      </Item>
    </List>
  </Menu>
</div>
