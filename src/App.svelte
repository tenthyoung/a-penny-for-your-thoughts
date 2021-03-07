<script>
  import { LottiePlayer } from "@lottiefiles/svelte-lottie-player";
  let isUserBroke = false;
  let brokeClickCount = 0;
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
    "I'm a little concerned about my buff friend in the back, he has a 12-pack. It seems a bit vain.",
    "When I roll out with the boys, you might have to hold the honeys back",
    "Who knew you could sell a thought?",
    "Stanley in the back brought his dinner to work... The nerve, but we gotta keep him on board since his dad funds us.",
  ];

  let controlsLayout = [
    "previousFrame",
    "playpause",
    "stop",
    "nextFrame",
    "progress",
    "frame",
    "loop",
    "spacer",
    "background",
    "snapshot",
    "zoom",
    "info",
  ];

  function handlePoorPerson() {
    isUserBroke = true;
    brokeClickCount++;

    if (brokeClickCount === brokeDialogue.length) {
      brokeClickCount = 0;
    }
  }
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
      height={300}
      {controlsLayout}
    />
  </div>
  <div class="dialogue">
    {#if isUserBroke}
      <p>{brokeDialogue[brokeClickCount]}</p>
    {:else}
      <p>{greeting}</p>
    {/if}
  </div>
  <div id="user-controls">
    <div
      class="money-button"
      data-to="tenthyoung@moneybutton.com"
      data-amount="0.01"
      data-label="For a thought"
      data-currency="USD"
    />
    <button class="secondary" on:click={handlePoorPerson}
      >I can't afford that</button
    >
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1rem;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    font-size: 4em;
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

  #lottie-wrap {
    height: 500px;
    overflow: hidden;
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

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
