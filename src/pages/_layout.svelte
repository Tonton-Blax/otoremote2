<script lang="ts">
  import Drawer, {
    AppContent,
    Content,
    Header,
    Title,
    Subtitle,
  } from '@smui/drawer';
  import Button, { Label } from '@smui/button';
  import List, { Item, Text } from '@smui/list';
 
  let open = false;
  let active = 'Gray Kittens';
 
  function setActive(value: string) {
    active = value;
  }
</script>


<!-- _layout.svelte -->
<div class="drawer-container">
  <Drawer variant="dismissible" bind:open>
    <Header>
      <Title>oTo</Title>
      <Subtitle>World's Best Teleprompter</Subtitle>
    </Header>
    <Content>
      <List>
        <Item
          href="javascript:void(0)"
          on:click={() => setActive('Gray Kittens')}
          activated={active === 'Gray Kittens'}
        >
          <Text>Gray Kittens</Text>
        </Item>
        <Item
          href="javascript:void(0)"
          on:click={() => setActive('A Space Rocket')}
          activated={active === 'A Space Rocket'}
        >
          <Text>A Space Rocket</Text>
        </Item>
        <Item
          href="javascript:void(0)"
          on:click={() => setActive('100 Pounds of Gravel')}
          activated={active === '100 Pounds of Gravel'}
        >
          <Text>100 Pounds of Gravel</Text>
        </Item>
        <Item
          href="javascript:void(0)"
          on:click={() => setActive('All of the Shrimp')}
          activated={active === 'All of the Shrimp'}
        >
          <Text>All of the Shrimp</Text>
        </Item>
        <Item
          href="javascript:void(0)"
          on:click={() => setActive('A Planet with a Mall')}
          activated={active === 'A Planet with a Mall'}
        >
          <Text>A Planet with a Mall</Text>
        </Item>
      </List>
    </Content>
  </Drawer>
 
  <AppContent class="app-content">
    <main class="main-content">
      <Button on:click={() => (open = !open)} >
        <Label>☰</Label></Button>
      <br />
      <slot>
        <!-- pages in this folder and subfolders
         will be rendered here -->
      </slot>
      <pre class="status">Active: {active}</pre>
    </main>
  </AppContent>
</div>
  
<style>
  /* These classes are only needed because the
    drawer is in a container on the page. */
  .drawer-container {
    position: relative;
    display: flex;
    height: 100%;
    overflow: hidden;
    z-index: 0;
  }
 
  * :global(.app-content) {
    flex: auto;
    overflow: auto;
    position: relative;
    flex-grow: 1;
    font-family: Roboto;
  }
 
  .main-content {
    overflow: auto;
    overflow-x:hidden;
    height: 100%;
    box-sizing: border-box;
  }
</style>