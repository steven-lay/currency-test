<script>
  let audInput = 1;

  let sgdRate = 0.8557;
  let myRate = 2.8036;
  let thaiRate = 21.4687;

  let customCurrency = 0;

  $: curSelection = "sg";

  $: aud = 0.0;

  function updateCurrency() {
    switch (curSelection) {
      case "sg":
        aud = (customCurrency / sgdRate).toFixed(2);
        break;
      case "my":
        aud = (customCurrency / myRate).toFixed(2);
        break;
      case "thai":
        aud = (customCurrency / thaiRate).toFixed(2);
        break;
    }
  }
</script>

<main>
  <h1>貨幣兌換器</h1>

  <form>
    <label for="audInput">澳幣: </label>
    <input id="audInput" type="number" bind:value={audInput} />
    <button
      on:click={() => {
        audInput = 1;
      }}>清除</button
    >
  </form>

  <h3>新幣：{(audInput * sgdRate).toFixed(2)}</h3>
  <h3>馬幣：{(audInput * myRate).toFixed(2)}</h3>
  <h3>泰銖：{(audInput * thaiRate).toFixed(2)}</h3>

  <hr />
  <hr />

  <form>
    <h3 for="selection">選擇貨幣:</h3>
    <select id="selection" bind:value={curSelection} on:change={updateCurrency}>
      <option value="sg">新幣</option>
      <option value="my">馬幣</option>
      <option value="thai">泰銖</option>
    </select>
    <input
      type="number"
      bind:value={customCurrency}
      on:input={updateCurrency}
    />
    <button
      on:click={() => {
        customCurrency = 0.0;
      }}>清除</button
    >
  </form>

  <h3>澳幣: ${aud}</h3>
</main>

<style>
  main {
    margin: 10px;
  }
</style>
