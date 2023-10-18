<script>
    import { afterUpdate } from "svelte";

    export let image
    export let name
    export let notes
    export let date
    export let create
    export let action

    const handleCreateSubmit = (event) => {
        if(action === 'create'){
            console.log("create a sign")
            create({image, name, date, notes})
        }
    }

</script>

<main>
    <div id=createForm>
        <form on:submit|preventDefault={handleCreateSubmit}>
            <input type="text" placeholder="Image Address" bind:value={image}/>
            <input type="test" placeholder="Name of Sign" bind:value={name}/>
            <textarea placeholder="Notes" bind:value={notes}/>
            <input type="submit" name="Add">
        </form>
    </div>
</main>