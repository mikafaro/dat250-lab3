<script>
    import { createEventDispatcher } from "svelte";
    import Button from "../shared/Button.svelte";

    let dispatch = createEventDispatcher();

    let fields = { question: '', option1: '', option2: ''}

    const submitHandler = () => {
        let poll = {...fields, votes1: 0, votes2: 0, id:Math.random()}
        dispatch('addPoll', poll);
    }
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question:</label>
        <input type="text" placeholder='Poll Question' id="question" bind:value={fields.question}>
    </div>
    <div class="form-field">
        <label for="option1">Option 1:</label>
        <input type="text" placeholder='Poll Option 1' id="option1" bind:value={fields.option1}>
    </div>
    <div class="form-field">
        <label for="option2">Option 2:</label>
        <input type="text" placeholder='Poll Option 2' id="option2" bind:value={fields.option2}>
    </div>
    <Button>Add Poll</Button>
</form>

<style>
    form{
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field{
        margin: 18px auto;
        text-align: left;
    }
    input{
        width: 100%;
        border-radius: 6px;
    }
    label{
        margin: 10px auto;
    }
</style>