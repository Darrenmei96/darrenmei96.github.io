<script>
  import { onMount } from "svelte";
  import confetti from "canvas-confetti";

  let yesPressed = false;
  let noCount = 0;

  function handleYes() {
    yesPressed = true;
    confetti({
      particleCount: 100,
      spread: 70,
      origin: { y: 0.6 },
    });
  }

  function handleNoClick() {
    noCount++;
  }

  $: noButtonStyle = `transform: scale(${Math.max(0, 1 - noCount * 0.1)})`;
  $: yesButtonStyle = `transform: scale(${1 + noCount * 0.2})`;
  $: subTitle = noCount === 0 ? "Quack quack? 🦆" : "Quack... 😢";
</script>

<main>
  <div class="container">
    {#if yesPressed}
      <div class="celebration">
        <h1 class="bounce">Chirp Chirp! Yay! 🐣</h1>
        <div class="gif-container">
          <!-- <img
            src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2QzM3MxM3MxM3MxM3MxM3MxM3MxM3MxM3MxMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/MDJ9IbxxvDUQM/giphy.gif"
            alt="Happy Cat"
          /> -->
          <img
            src="https://media.tenor.com/wcDQ5VaLa9MAAAAi/bubu-dudu.gif"
            alt="Happy bubu"
          />
        </div>
        <p>You've made me the happiest bird! 💖</p>
      </div>
    {:else}
      <div class="proposal">
        <div class="gif-container">
          <!-- <img
            src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2QzM3MxM3MxM3MxM3MxM3MxM3MxM3MxM3MxMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3oriO0OEd9QIDdllqo/giphy.gif"
            alt="Cute begging"
          /> -->
          <img
            src="https://media.tenor.com/0cNM_9li440AAAAj/dudu-giving-flowers-bubu-flowers.gif"
            alt="bubu give flowers"
          />
        </div>
        <h1>Will you be my Valentine, Birdie?</h1>
        <p class="subtitle">{subTitle}</p>
        <div class="buttons">
          <button class="yes-btn" style={yesButtonStyle} on:click={handleYes}>
            Yes
          </button>

          <button class="no-btn" style={noButtonStyle} on:click={handleNoClick}>
            No
          </button>
        </div>
      </div>
    {/if}
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: "Comic Sans MS", "Chalkboard SE", sans-serif; /* Playful font */
    background-color: #ffe6e6;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
  }

  .container {
    text-align: center;
    background: white;
    padding: 2rem;
    border-radius: 20px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    max-width: 90%;
    width: 400px;
  }

  h1 {
    color: #ff3366;
    margin-bottom: 2rem;
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1.5rem;
    color: #555;
    margin-bottom: 2rem;
    font-style: italic;
  }

  .buttons {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  button {
    padding: 1rem 2rem;
    font-size: 1.2rem;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: bold;
    min-width: 100px;
  }

  .yes-btn {
    background-color: #28a745;
    color: white;
  }

  .yes-btn:hover {
    transform: scale(1.1);
    box-shadow: 0 5px 15px rgba(40, 167, 69, 0.4);
  }

  .no-btn {
    background-color: #dc3545;
    color: white;
  }

  /* When it becomes 'Yes' style via JS, we might want to match the green */

  .gif-container img {
    width: 100%;
    max-height: 200px;
    object-fit: contain;
    border-radius: 10px;
    margin-bottom: 1rem;
  }

  .celebration p {
    font-size: 1.5rem;
    color: #555;
  }

  .bounce {
    animation: bounce 1s infinite alternate;
  }

  @keyframes bounce {
    from {
      transform: translateY(0);
    }
    to {
      transform: translateY(-10px);
    }
  }
</style>
