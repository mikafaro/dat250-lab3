<script>
    import Card from "../shared/Card.svelte";

    export let poll;
    export let votes;

    const voteURL = "http://localhost:8080/votes";


    // reative values
    
   // @ts-ignore
   //  $: percent1 = Math.floor(100 / totalVotes * votes1);
   const totalVotes = 0;
   const percent1 = 0;
   const percent2 = 0;
   // @ts-ignore
   //  $: percent2 = Math.floor(100 / totalVotes * votes2);

    async function handleVote(opt, id) {
        const vote = {
            "pollId" : id,
            "optId": opt,
        }
        try {
            const response = await fetch(voteURL, {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: JSON.stringify(vote)
            });

            if (response.ok) {
                const data = await response.json();
                alert("Vote created")
            } else {
                console.error("Could not create vote", response.statusText);
                alert("Could not create vote");
            }
        } catch (error) {
            console.error("Error creating vote", error);
            alert("Could not create vote");
        }
    }
</script>

<Card>
    <div class="poll">
        <h3> {poll.question}</h3>
        <p>Total votes: { totalVotes }</p>
        <div class="option" on:click={() => handleVote(1, poll.id)}>
            <div class="percent percent-1" style="width: {percent1}%"></div>
            <span>{ poll.option1 } ({ poll.votes1 })</span>
        </div>
        <div class="option" on:click={() => handleVote(2, poll.id)}>
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