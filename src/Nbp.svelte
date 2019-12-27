<script>
  import { onMount } from "svelte";

  let kurs, wy, wynik;
  let ile = "";
  let max = 9999999999;
  const opts = [
    "EUR",
    "USD",
    "GBP",
    "CHF",
    "UAH",
    "RUB",
    "BYN",
    "CZK",
    "HUF",
    "NOK",
    "SEK",
    "DKK",
    "ISK",
    "CNY"
  ];
  let op = opts[0];
  let tabela = "a";

  onMount(async () => {
    const res = await fetch(
      `https://api.nbp.pl/api/exchangerates/rates/a/${op}/?format=json`
    );
    let ph = await res.json();
    return (kurs = ph.rates[0].mid);
  });

  $: kantor(op);
  $: if (ile > max) {
    alert("A Ty łobuzie! Podziel sie z wujkiem Pepsonem :)");
  }
  function kantor(op) {
    if(op == "BYN"){
      tabela="b"
    }
    let waluta = `https://api.nbp.pl/api/exchangerates/rates/${tabela}/${op}/?format=json`;
    fetch(`${waluta}`)
      .then(r => r.json())
      .then(data => {
        kurs = data.rates[0].mid;
        wy = kurs * ile;
        return (wynik = parseFloat(wy).toFixed(2));
      });
  }

  const licz = () => {
    wy = kurs * ile;
    return (wynik = parseFloat(wy).toFixed(2));
  };

  // $: console.log("ile =", ile);
</script>

<br />
<input bind:value={ile} type="number" placeholder="1" on:input={licz} />
<select bind:value={op}>
  {#each opts as op}
    <option {op}>{op}</option>
  {/each}
</select>
<br />
<br />
{#if ile}
  <h1>{ile} {op} = {wynik} zł</h1>
{/if}
<h1>{kurs ? kurs : 'Ładowanie...'} kurs {op}</h1>
