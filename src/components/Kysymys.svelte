<script>
  export let kysymys; //nykyinen kysymys
  export let seuraava; //funktio seuraavaan kysymykseen siirtymiseen
  export let nykyinen; //nykyisen kysymyksen numero
  export let maksimi; //kysymysten kokonaismäärä

  let vastausValittu = false; //tila, jossa käyttäjä on valinnut vastauksen
  let vastausOikein = false; //tieto siitä, oliko vastaus oikein

  //funktio, joka tarkistaa, onko käyttäjän valitsema vastaus oikea
  function tarkistaVastaus(vastausIndex) {
    vastausValittu = true;
    vastausOikein = vastausIndex === kysymys.oikea;
  }

  //funktio, joka siirtyy seuraavaan kysymykseen
  function siirrySeuraavaan() {
    seuraava(vastausOikein);
    vastausValittu = false;
    vastausOikein = false;
  }
</script>

<div class="kysymys">
  <!-- Näytetään nykyisen kysymyksen numero -->
  <p class="numerointi">Kysymys {nykyinen}/{maksimi}</p>
  <!-- Kysymys teksti -->
  <p>{kysymys.kysymys}</p>
  <div class="vastaukset">
    <!-- Vastausvaihtoehdot, vastauksen tarkistaminen, painikkeiden disablointi, vastausten korostaminen -->
    {#each kysymys.vastaukset as vastaus, index}
      <button
        on:click={() => tarkistaVastaus(index)}
        disabled={vastausValittu}
        class:valittu={vastausValittu && index === kysymys.oikea}
        class:vaara={vastausValittu &&
          index !== kysymys.oikea &&
          index === index}
      >
        {vastaus}
      </button>
    {/each}
  </div>
  <!-- Näytetään palaute ja nappi seuraavaan kysymykseen siirtymiseen-->
  {#if vastausValittu}
    <p class={vastausOikein ? 'oikein' : 'vaarin'}>
      {vastausOikein ? 'Oikein!' : 'Väärin.'}
    </p>
    <button on:click={siirrySeuraavaan}>Seuraava kysymys</button>
  {/if}
</div>
