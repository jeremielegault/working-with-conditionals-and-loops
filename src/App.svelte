<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";
  let createdContacts = [];

  function addContactCard() {
    if (
      name.trim().length == 0 ||
      title.trim().length == 0 ||
      image.trim().length == 0 ||
      description.trim().length == 0
    ) {
      formState = "INVALID";
      return;
    }
    createdContacts = [
      ...createdContacts,
      {
        name: name,
        jobTitle: title,
        imageUrl: image,
        desc: description,
      },
    ];
    formState = "done";
  }
</script>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>
<button on:click={addContactCard}>Add Contact Card</button>
{#if formState == "INVALID"}
  <h1>YOU MUST FINISH THE FORM</h1>
{:else}
  <p>please enter some data and click the button to submit</p>
{/if}
{#each createdContacts as contact}
  <ContactCard
    userName={contact.name}
    jobTitle={contact.jobTitle}
    description={contact.desc}
    userImage={contact.imageUrl}
  />
{/each}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
