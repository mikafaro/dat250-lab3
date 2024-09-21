<script>
    import Button from "../shared/Button.svelte";

    let fields = { question: '', option1: '', option2: ''}

    const submitHandler = () => {
        let poll = {
            "question": fields.question,
            "options": [
                {
                    "caption": fields.option1,
                    "presentationOrder": 1,
                },
                {
                    "caption" : fields.option2,
                    "presentationOrder": 2,
                }
            ]
        }
        submitPoll(poll);
    }

    async function submitPoll(poll) {
        try {
            const response = await fetch('http://localhost:8080/polls', {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: JSON.stringify(poll)
            });

            if (response.ok) {
                const data = await response.json();
                alert("Poll created")
            } else {
                console.error("Could not create poll", response.statusText);
                alert("Could not create poll");
            }
        } catch (error) {
            console.error("Error creating poll", error);
            alert("Could not create poll");
        }
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