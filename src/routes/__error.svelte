<script context="module">
  /** @type { import('@sveltejs/kit').ErrorLoad } */
  export function load({ error, status }) {
    return {
      props: {
        title: `${status}: ${error.message}`
      }
    }
  }
</script>

<script>
  export let title
</script>

<svelte:head>
  <title>404: Not Found</title>
</svelte:head>

<section>
  <h1>{title}</h1>
  <p>Oops, doesn't exist!</p>
</section>

<style>
  h1 {
    color: tomato;
  }
</style>
