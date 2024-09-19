<script>
    import Footer from "./components/Footer.svelte";
    import Header from "./components/Header.svelte";
    import Tabs from "./shared/Tabs.svelte";
    import CreatePollForm from "./components/CreatePollForm.svelte";
    // @ts-ignore
    import PollList from "./components/PollList.svelte";

    // tabs
    let items = ['Active Polls', 'New Poll'];
    let activeItem = 'Active Polls';

    const tabChange = (e) => {
      activeItem = e.detail;
    }

    let polls = [
      {
        id: 1,
        question: 'Is this a great poll?',
        option1: 'yes',
        option2: 'no',
        votes1: 2,
        votes2: 8,
      },
    ];

    const addPollHandler = (e) => {
      const poll = e.detail;
      polls = [poll, ...polls];
      activeItem = 'Active Polls';
    }

    const handleVote = (e) => {
      const { option, id } = e.detail;
      let pollsCopy = [...polls];
      let upvotedPoll = pollsCopy.find((poll) => poll.id == id);

      if (option === 'option1'){
        upvotedPoll.votes1++;
      }
      if (option === 'option2'){
        upvotedPoll.votes2++;
      }
      polls = pollsCopy;
    }

</script>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange}/>
  {#if activeItem === 'Active Polls'}
    <PollList {polls} on:vote={handleVote} />
  {:else if activeItem === 'New Poll'}
    <CreatePollForm on:addPoll={addPollHandler} />
  {/if}
</main>
<Footer />

<style>
  main{
    max-width: 960px;
    margin: 40px auto;
  }
</style>
