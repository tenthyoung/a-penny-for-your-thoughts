<script>
  export let name;
</script>

<main>
  <h1>A penny for my thoughts?</h1>
  <p>
    Send me a penny, and I'll tell you what I'm thinking about the right now...
  </p>
  <div
    class="money-button"
    data-to="[paymail, user ID, address, or script]"
    data-amount="[amount]"
    data-currency="[currency]"
  />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
