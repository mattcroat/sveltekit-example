<script context="module">
  /** @type { import('@sveltejs/kit').Load } */
  export async function load({ fetch }) {
    const url = 'https://api.github.com/gists/public'
    const response = await fetch(url)

    if (!response.ok) {
      return {
        status: response.status,
        error: new Error(`Could not load ${url}`)
      }
    }

    return {
      props: {
        gists: await response.json()
      }
    }
  }
</script>

<script lang="ts">
  interface Gist {
    url: string
    description: string
    files: {
      [key: string]: unknown
    }
  }

  export let gists: Gist[]
</script>

<svelte:head>
  <title>Home</title>
</svelte:head>

<main>
  <h1>Gists</h1>

  <ul>
    {#each gists as gist (gist.url)}
      <li>
        <a href={gist.url}>{Object.keys(gist.files)[0]} ({gist.description})</a>
      </li>
    {/each}
  </ul>
</main>
