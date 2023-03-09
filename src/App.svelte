<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
	let formState = '';

  let createContact = [];
	let addConstract = () => {
		if (name.trim().length==0 || title.trim().length == 0 || image.trim().length == 0 || description.trim().length == 0)
    {
      formState = 'invalid';
      return;
    }
    createContact = [
      ...createContact,
      {
        name: name, 
        jobTitle: title, 
        imageUrl: image, 
        desc: description
      }]
		formState = 'done';
	}

  let deleteFirst = () => {
    createContact = createContact.slice(1);
  }

  let deleteLast = () => {
    createContact = createContact.slice(0, -1);
  }
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

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

<button on:click={addConstract}>카드추가</button>
<button on:click={deleteFirst}>첫번째 카드제거</button>
<button on:click={deleteLast}>마지막 카드제거</button>
{#if formState === 'invalid'}
  <p>데이터를 다 입력후 눌러주세요!!</p>
{:else}
  <p>데이터를 입력후 눌러주세요</p>
{/if}

{#each createContact as contact}
<ContactCard 
    userName={contact.name} 
    jobTitle={contact.jobTitle} 
    description = {contact.desc} 
    userImage={contact.imageUrl} 
/>
{:else}
  <p>번호를 모르니까 번호를 입력해주세요</p>  
{/each}