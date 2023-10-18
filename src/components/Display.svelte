<script>
    export let signs
    export let image
    export let name
    export let notes
    export let date
    export let update
    export let action
    export let select
    export let id
    export let destroy
    export let reset
    export let showUpdateForm


    const handleUpdateSubmit = (event) => {
        if(action === 'update'){
            console.log("update a sign")
            update({image, name, date, notes, id})
        }
    }

</script>

<div>
    <ul>
        {#each signs as sign}
            
            <div id="signCard">
                <li>
                    
                    <div id="imgContainer">
                        <img src={sign.image} alt={sign.name}/>
                    </div>

                    <div id="cardDetails">
                        <h2>"{sign.name}"</h2>
                        {#if sign.notes != false}
                            <h3>Notes: {sign.notes}</h3>
                        {/if}
                        <h4>Created: {sign.date}</h4>
                    </div>

                    <div id='delete-edit-buttons'>
                        <div id='deleteButton'><button on:click={destroy(sign)}>Delete</button></div>
                        <button on:click={select(sign)}>Edit</button>
                    </div>

                    {#if showUpdateForm}    
                        <div id="updateForm"> 
                            <form on:submit|preventDefault={handleUpdateSubmit}>
                                <input type="text" placeholder="Image Address" name="image" bind:value={image}/>
                                <input type="test" placeholder="Name of Sign" name="name" bind:value={name}/>
                                <textarea placeholder="Notes" name="notes" bind:value={notes}/>
                                <div id="save-cancel-buttons">
                                    <button>Save</button>
                                    <button on:click={reset(sign)}>Cancel</button>
                                </div>
                            </form>
                        </div>   
                    {/if}

                </li>
            </div>
        {/each}
    </ul>

</div>
