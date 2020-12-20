<script>
    import {createEventDispatcher} from 'svelte';
    const dispatch = createEventDispatcher();

    export let username;

    import { scale} from 'svelte/transition';
</script>

<header >
    <div class="container" in:scale={{duration:500}}>
        <div class="row">
            <div class="col-md">
                <h1>Search For Instagram Account</h1>

                <div class="form-group">
                    <input type="text" class="form" bind:value="{username}" placeholder="Cari Username ...">
                    <button on:click={()=> dispatch("onClickSearch", username)}>Search</button>
                </div>
            </div>
        </div>
    </div>
</header>

<style>
    header{
        background-color: #fafafa;
        padding:20px;
        text-align: center;
    }
</style>