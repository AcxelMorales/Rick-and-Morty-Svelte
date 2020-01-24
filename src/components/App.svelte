<script>
  import { onMount } from "svelte";

  const API = "https://rickandmortyapi.com/api/character";

  let data = [];
  let characters = [];

  onMount(async () => {
    const res = await fetch(API);
    data = await res.json();
    console.log(data);
    characters = data.results;
  });
</script>

<style>
  .characters {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
  }

  img {
    width: 100%;
    margin: 0;
  }

  .card-title {
    font-size: 1.4em;
    color: rgb(87, 87, 87);
  }

  .collection {
    margin-top: 15px;
  }
</style>

<div class="characters">
  {#each characters as character}
    <!-- <figure>
      <img src={character.image} alt={character.name} />
      {#if character.gender === 'Male'}
        <span class="new badge" data-badge-caption="">{character.gender}</span>
      {:else if character.gender === 'Female'}
        <span class="new badge pink" data-badge-caption="">
          {character.gender}
        </span>
      {:else}
        <span class="new badge purple" data-badge-caption="">
          {character.gender}
        </span>
      {/if}
      <figcaption>{character.name}</figcaption>
    </figure> -->

    <div class="card">
      <div class="card-image waves-effect waves-block waves-light">
        <img src={character.image} alt={character.name} />
      </div>
      <div class="card-content grey lighten-4">
        <span class="card-title dark-text activator">
          {character.name}
          <i class="material-icons right grey-text">more_vert</i>
        </span>
      </div>
      <div class="card-reveal">
        <span class="card-title dark-text">
          {character.name}
          <i class="material-icons red-text right">close</i>
        </span>
        <div class="collection">
          <a href="#!" class="collection-item">
            {#if character.gender === 'Male'}
              <span class="new badge blue" data-badge-caption="">
                {character.gender}
              </span>
              Gender
            {:else if character.gender === 'Female'}
              <span class="new badge pink" data-badge-caption="">
                {character.gender}
              </span>
              Gender
            {:else}
              <span class="new badge purple" data-badge-caption="">
                {character.gender}
              </span>
              Gender
            {/if}
          </a>
          <a href="#!" class="collection-item">
            {#if character.status === 'Alive'}
              <span class="new badge green" data-badge-caption="">
                {character.status}
              </span>
              Alive
            {:else}
              <span class="new badge red" data-badge-caption="">
                {character.status}
              </span>
              Alive
            {/if}
          </a>
          <a href="#!" class="collection-item">
            <span class="new badge orange" data-badge-caption="">
              {character.species}
            </span>
            Species
          </a>
          <a href="#!" class="collection-item">
            <span class="new badge grey" data-badge-caption="">
              {character.origin.name}
            </span>
            Origin
          </a>
        </div>
      </div>
    </div>
  {:else}
    <p>loading...</p>
  {/each}
</div>
