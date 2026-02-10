<script>
  import { onMount } from 'svelte';
  import confetti from 'canvas-confetti';

  let yesPressed = false;
  let noButtonText = "No";
  let noButtonStyle = "";
  
  function handleYes() {
    yesPressed = true;
    confetti({
      particleCount: 100,
      spread: 70,
      origin: { y: 0.6 }
    });
  }

  function handleNoHover() {
    noButtonText = "Yes";
    // Optional: make it look exactly like the Yes button
    noButtonStyle = "background-color: #ff3e00; transform: scale(1.1);";
  }

  function handleNoLeave() {
    // Optional: revert capability? 
    // The user said "turn into a yes", usually implies permanent or while interacting. 
    // Let's keep it as Yes once hovered to ensure success :)
    // or revert if they leave to be cheeky? 
    // "When the no button is hovered over or pressed, it should turn into a yes"
    // implies state change. Let's make it permanent for this session.
  }

  function handleNoClick() {
    handleYes();
  }
</script>

<main>
  <div class="container">
    {#if yesPressed}
      <div class="celebration">
        <h1 class="bounce">Yay! 💖</h1>
        <div class="gif-container">
          <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2QzM3MxM3MxM3MxM3MxM3MxM3MxM3MxM3MxMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/MDJ9IbxxvDUQM/giphy.gif" alt="Happy Cat" />
        </div>
        <p>You've made me the happiest person!</p>
      </div>
    {:else}
      <div class="proposal">
        <div class="gif-container">
           <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2QzM3MxM3MxM3MxM3MxM3MxM3MxM3MxM3MxMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3oriO0OEd9QIDdllqo/giphy.gif" alt="Cute begging" />
        </div>
        <h1>Will you be my Valentine?</h1>
        <div class="buttons">
          <button class="yes-btn" on:click={handleYes}>
            Yes
          </button>
          
          <button 
            class="no-btn" 
            style={noButtonStyle}
            on:mouseenter={handleNoHover}
            on:click={handleNoClick}
          >
            {noButtonText}
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
    font-family: 'Comic Sans MS', 'Chalkboard SE', sans-serif; /* Playful font */
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
    box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    max-width: 90%;
    width: 400px;
  }

  h1 {
    color: #ff3366;
    margin-bottom: 2rem;
    font-size: 2rem;
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
    from { transform: translateY(0); }
    to { transform: translateY(-10px); }
  }
</style>
