<script>
  import Kysymys from './components/Kysymys.svelte';
  import './app.css';

  //Tietovisan kysymykset ja vastaukset

  let kysymykset = [
    {
      kysymys: 'Mikä on Suomen pääkaupunki?',
      vastaukset: ['Oulu', 'Tampere', 'Turku', 'Helsinki'],
      oikea: 3,
    },
    {
      kysymys: 'Mikä on kemiallinen kaava veden molekyylille?',
      vastaukset: ['H2O', 'CO2', 'O2', 'NH3'],
      oikea: 0,
    },
    {
      kysymys: 'Mikä on maailman suurin valtameri?',
      vastaukset: ['Atlantti', 'Tyynimeri', 'Intian valtameri', 'Jäämeri'],
      oikea: 1,
    },
    {
      kysymys: 'Kuka on Yhdysvaltojen nykyinen presidentti?',
      vastaukset: [
        'Kamala Harris',
        'Joe Biden',
        'John Kennedy',
        'Donald Trump',
      ],
      oikea: 1,
    },
    {
      kysymys: 'Mikä on maailman nopein eläin?',
      vastaukset: ['Susi', 'Gebardi', 'Leijona', 'Haukka'],
      oikea: 1,
    },
  ];

  let nykyinenKysymys = 0; //Seuraa, mikä kysymys on vuorossa
  let pisteet = 0; //Käyttäjän keräämät pisteet

  //funktio seuraavan kysymyksen näyttämiseksi
  function seuraavaKysymys(onOikein) {
    if (onOikein) pisteet++;
    nykyinenKysymys++;
  }

  //funktio tietovisan aloitukseen uudelleen
  function alustaUudelleen() {
    nykyinenKysymys = 0;
    pisteet = 0; //nollataan pisteet ja aloitetaan alusta
  }
</script>

<main>
  <h1>Eetun Tietovisa</h1>

  <!-- Näytetään kysymykset tai lopputulos riippuen tilanteesta -->
  {#if nykyinenKysymys < kysymykset.length}
    <!-- Kysymys-komponentti, joka näyttää nykyisen kysymyksen -->
    <Kysymys
      kysymys={kysymykset[nykyinenKysymys]}
      seuraava={seuraavaKysymys}
      nykyinen={nykyinenKysymys + 1}
      maksimi={kysymykset.length}
    />
  {:else}
    <!-- Lopputuloksen näyttäminen, kun kaikki kysymykset on käyty -->
    <div class="tulokset">
      <p>Tietovisa ohi! Sait {pisteet}/{kysymykset.length} pistettä.</p>
      <button on:click={alustaUudelleen}>Aloita alusta</button>
    </div>
  {/if}
</main>
