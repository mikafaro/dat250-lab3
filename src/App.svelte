<script>
    import Footer from "./components/Footer.svelte";
    import Header from "./components/Header.svelte";
    import Tabs from "./shared/Tabs.svelte";
    import CreatePollForm from "./components/CreatePollForm.svelte";
    // @ts-ignore
    import PollList from "./components/PollList.svelte";
    import { onMount } from "svelte";

    // tabs
    let items = ['Active Polls', 'New Poll'];
    let activeItem = 'Active Polls';

    const tabChange = (e) => {
      activeItem = e.detail;
    }

    let polls = [];
    let votes = new Map();

    const pollURL = "http://localhost:8080/polls";
    const voteURL = "http://localhost:8080/votes";

    onMount(() => {
      async function fetchData() {
        const response = await fetch(pollURL);
        if (!response.ok) {console.log("could not fetch poll data")}
        const data = await response.json();
        // const vote_response = await fetch(voteURL);
        // if (!vote_response.ok) {console.log("could not fetch vote data")}
        //const vote_data = await vote_response.json();
        polls = data;
        // votes = vote_data;
      }
      
      const interval = setInterval(fetchData, 3000);
      fetchData();

      return () => clearInterval(interval);
    });

</script>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange}/>
  {#if activeItem === 'Active Polls'}
    <PollList {polls} {votes} />
  {:else if activeItem === 'New Poll'}
    <CreatePollForm  />
  {/if}
</main>
<Footer />

<style>
  main{
    max-width: 960px;
    margin: 40px auto;
  }
</style>
