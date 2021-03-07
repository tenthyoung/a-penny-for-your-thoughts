<script>
  import { LottiePlayer } from "@lottiefiles/svelte-lottie-player";
  let isUserBroke = false;
  let userCanAfford = "unknown";
  let brokeClickCount = 0;
  let thoughtCount = -1;
  let showMoneyButton = true;

  const greeting =
    "Alright, pay me a penny for a thought. Buy now while the sale lasts.";
  const brokeDialogue = [
    "This ain't no charity. A penny for a thought. Deal ends soon.",
    "You can't afford a penny? Are you frugal or you lie??",
    "You want me to lower the price? Nice try, ain't happenin'.",
    "It's pretty easy to get a penny. I'm starting to believe you have a penny, but you're lying. And that's wrong.",
    "Look man, a guy's gotta eat. You see Stanley over there only has a bone for dinner. Pay us a penny, and I'll give him a steak.",
    "Is this how you haggle..? You just keep telling us you can't afford it. Ain't gonna work, mate.",
  ];
  const thoughts = [
    "What am I thinking..? I'm a little concerned about my buff friend in the back, he has a 12-pack. It seems a bit vain.",
    "When I roll out with the boys, you might have to hold the honeys back",
    "Stanley in the back brought his lunch to work... The nerve, but we gotta keep him on board since his dad funds us.",
    "My final thought... thanks for being a valuable customer. I'm all out of thoughts.",
  ];

  function handlePoorPerson() {
    isUserBroke = true;
    brokeClickCount++;

    if (brokeClickCount === brokeDialogue.length) {
      brokeClickCount = 0;
    }
  }

  function userPaidAPenny(payment) {
    thoughtCount++;
    userCanAfford = true;

    if (thoughtCount === thoughts.length - 1) {
      showMoneyButton = false;
    }
  }

  $: console.log(thoughtCount);
</script>

<main>
  <h1>A penny for your thoughts?</h1>
  <div id="lottie-wrap" class="center">
    <LottiePlayer
      src="https://assets4.lottiefiles.com/packages/lf20_0p21PY.json"
      autoplay={true}
      loop={true}
      renderer="svg"
      background="transparent"
    />
  </div>
  <div class="dialogue">
    {#if isUserBroke}
      <p>{brokeDialogue[brokeClickCount]}</p>
    {:else if userCanAfford === true}
      <p>{thoughts[thoughtCount]}</p>
    {:else}
      <p>{greeting}</p>
    {/if}
  </div>
  <div id="user-controls">
    {#if showMoneyButton}
      <div
        class="money-button"
        data-to="tenthyoung@moneybutton.com"
        data-amount="0.01"
        data-label="For a thought"
        data-currency="USD"
        data-on-payment="userPaidAPenny"
      />
    {/if}
    {#if userCanAfford === "unknown"}
      <button class="secondary" on:click={handlePoorPerson}
        >I can't afford that</button
      >
    {/if}
  </div>
</main>

<style>
  main {
    margin: 0 auto;
    text-align: center;
    width: 100%;
  }

  h1 {
    color: #ff3e00;
    font-size: 3rem;
    font-weight: 100;
  }

  .center {
    width: fit-content;
    margin: 0 auto;
  }

  .dialogue {
    height: 3rem;
    max-width: 600px;
    margin: 0 auto;
    padding: 0 1rem;
    font-size: 1rem;
  }

  .dialogue p {
    line-height: 1.2;
  }

  .money-button {
    width: 11rem !important;
  }

  #user-controls {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem 0;
  }

  #user-controls button {
    margin-top: 1rem;
  }
</style>
