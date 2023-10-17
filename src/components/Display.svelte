<script>
    export let signs
    export let image
    export let name
    export let notes
    export let date
    export let update
    export let action
    export let select
    export let showUpdateForm
    export let id
    export let destroy
    export let reset


    const handleUpdateSubmit = (event) => {
        
        event.preventDefault()

        if(action === 'update'){
            console.log("update a sign")
            update({image, name, date, notes, id})
        }
    }

</script>

<div>
    <ul>
        {#each signs as sign}
            <li>
                <div id="signCard">
                    <img src={sign.image} alt={sign.name}/>
                    <h1>{sign.name}</h1>
                    {#if sign.notes != false}
                        <h2>Notes: {sign.notes}</h2>
                    {/if}
                    <h4>Created: {sign.date}</h4>
                    <button on:click={destroy(sign)}>Delete</button>
                    <button on:click={select(sign)}>Edit</button>

                    {#if showUpdateForm}
                        {#if sign.id = showUpdateForm}    
                        <form on:submit={handleUpdateSubmit}>
                                <input type="text" placeholder="Image Address" bind:value={image}/>
                                <input type="test" placeholder="Name of Sign" bind:value={name}/>
                                <input type="text"  placeholder="Notes" bind:value={notes}/>
                                <button>Save</button>
                                <button on:click={reset(sign)}>Cancel</button>
                            </form>
                        {/if}
                    {/if}
                </div>
            </li>
        {/each}
    </ul>

</div>
