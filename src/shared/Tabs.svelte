<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    export let items;
    export let activeItem;
</script>

<div class="tabs">
    <ul>
        {#each items as item}
            <li on:click={() => dispatch('tabChange', item)}>
                <div class:active={item === activeItem}>{item}</div>
            </li>
        {/each}
    </ul>
</div>

<style>
    .tabs{
        margin-bottom: 40px;
    }
    ul{
        display: flex;
        justify-content: center;
        padding: 0;
        list-style-type: none;
    }
    li{
        margin: 0 16px;
        font-size: 20px;
        color: #c0cfb2;
        cursor: pointer;
    }
    .active{
        color: #44624a;
        border-bottom: 2px solid #44624a;
        padding-bottom: 8px;
    }
</style>