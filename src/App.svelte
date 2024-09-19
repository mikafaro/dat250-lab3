<script>
    import Footer from "./components/Footer.svelte";
    import Header from "./components/Header.svelte";
    import Tabs from "./shared/Tabs.svelte";

    // tabs
    let items = ['Active Polls', 'New Poll'];
    let activeItem = 'Active Polls';

    const tabChange = (e) => {
      activeItem = e.detail;
    }
</script>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange}/>
  {#if activeItem === 'Active Polls'}
    <p>Poll list component here</p>
  {:else if activeItem === 'New Poll'}
    <p>New poll component here</p>
  {/if}
</main>
<Footer />

<style>
  main{
    max-width: 960px;
    margin: 40px auto;
  }
</style>
