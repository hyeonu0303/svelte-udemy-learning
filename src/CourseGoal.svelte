<script>
  export let goal;
  
  $: doHighlight = goal.includes('i');
</script>

<style>
  .highlight {
    color: red;
  }
</style>

<h1 class:hightlight = {doHighlight}>{goal}></h1>
