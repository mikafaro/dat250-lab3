<script>
    import { createEventDispatcher } from "svelte";
    import Card from "../shared/Card.svelte";

    export let poll;

    const dispatch = createEventDispatcher();

    // reative values
    $: totalVotes = poll.votes1 + poll.votes2;
    $: percent1 = Math.floor(100 / totalVotes * poll.votes1);
    $: percent2 = Math.floor(100 / totalVotes * poll.votes2);

    const handleVote = (option, id) => {
        dispatch('vote', {option, id});
    }
</script>

<Card>
    <div class="poll">
        <h3> {poll.question}</h3>
        <p>Total votes: { totalVotes }</p>
        <div class="option" on:click={() => handleVote('option1', poll.id)}>
            <div class="percent percent-1" style="width: {percent1}%"></div>
            <span>{ poll.option1 } ({ poll.votes1 })</span>
        </div>
        <div class="option" on:click={() => handleVote('option2', poll.id)}>
            <div class="percent percent-2" style="width: {percent2}%"></div>
            <span>{ poll.option2 } ({ poll.votes2 })</span>
        </div>
    </div>
</Card>

<style>
    h3{
        margin: 0 auto;
        color: #8ba888;
    }
    p{
        margin-top: 6px;
        font-size: 14px;
        margin-bottom: 30px;
    }
    .option{
        background: #c0cfb2;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
        border-radius: 20px;
    }
    .option:hover{
        opacity: 0.6;
    }
    span{
        display: inline-block;
        padding: 10px 20px;
    }
    .percent{
        height: 100%;
        position: absolute;
        box-sizing: border-box;
        opacity: 0.2;
        border-radius: 20px;
    }
    .percent-1{
        background: red;
    }
    .percent-2{
        background: blue;
    }
</style>