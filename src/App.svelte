<script>
  import { onMount } from "svelte";
  import Display from "./components/Display.svelte";
  import Form from "./components/Form.svelte";

  const url = 'https://capstoneback-z300.onrender.com/signs/'

  /////////// Set state components /////////////////////////////////////////////////////
    let id = ""  
    let image = ""
    let name = ""
    let notes = ""
    let date = "" //date will be auto poppulated when a sign is created
    let action = "create"
    let signs = []
    let showCreateForm = false
    let showUpdateForm = false


  ///FUNCTIONS///////////////////////////////////////////////////////////////////////////

  //TOGGLE FORMS
    const toggleCreateForm = () => {
      showCreateForm = !showCreateForm
    }

    const toggleUpdateForm = () => {
      showUpdateForm = !showUpdateForm
    }
  
  //RESET STATE
    const resetState = () => {
      id = ''
      image = ''
      name = ''
      notes = ''
      date = ''
      action = 'create'
      showCreateForm = false
      showUpdateForm = false
    }

  //GET ALL SIGNS
    const getSigns = async() => {
      const response = await fetch(url)
      const data = await response.json()
      signs = data
    }

  //CREATE A SIGN
    const createSign = async (sign) => {
      await fetch(url, {
        method: 'post',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(sign)
      })
      getSigns()
      resetState()
    }


    //SELECT A SIGN TO UPDATE
      const selectSign = async (sign) => {
        showUpdateForm = true
        id = sign.id
        image = sign.image
        name = sign.name
        date = sign.date
        notes = sign.notes
        action = 'update'
      }

  //UPDATE A SIGN
    const updateSign = async (sign) => {
      await fetch(url + `${sign.id}/`, {
        method: 'put',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(sign)
      })
      getSigns()
      resetState()
    }

  //DELETE A SIGN
    const deleteSign = async (sign) => {
      await fetch(url + `${sign.id}/`, {
        method: 'delete'
      })
      getSigns()
      resetState()
    }


//////////////////////////////////////////////////////////////////////////////
  
// lifecycle
  onMount(() => {getSigns()})

</script>

<main>

  <h1>ASLex</h1>
  <button on:click={toggleCreateForm}>Add Sign</button>
  
  {#if showCreateForm}
    <Form
      image={image}
      action={action}
      name={name}
      date={date}
      notes={notes}
      create={createSign}
    />
  {/if}
  
    <Display
      signs={signs}
      image={image}
      action={action}
      name={name}
      date={date}
      notes={notes}
      update={updateSign}
      select={selectSign}
      showUpdateForm={showUpdateForm}
      id={id}
      destroy={deleteSign}
      reset={resetState}
    />

</main>

