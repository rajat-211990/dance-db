<script>
  import { goto } from '$app/navigation';

  function handleLogin() {
    goto('/login');
  }
</script>

<style>
  .hero {
    min-height: 100vh;
    background: linear-gradient(135deg, #1a1a1a, #121212);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 2rem;
    color: white;
    animation: fadeIn 1s ease-out;
  }

  h1 {
    font-size: 4rem;
    font-weight: 300;
    letter-spacing: 2px;
    margin-bottom: 1rem;
    font-family: 'Segoe UI Light', sans-serif;
    color: #f3f3f3;
  }

  p {
    font-size: 1.2rem;
    color: #ccc;
    margin-bottom: 2rem;
  }

  button {
    padding: 0.75rem 2rem;
    font-size: 1.1rem;
    background-color: #6366f1;
    border: none;
    color: white;
    font-weight: 600;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.2s ease;
  }

  button:hover {
    background-color: #4f46e5;
  }

  @keyframes fadeIn {
    0% {
      opacity: 0;
      transform: translateY(40px);
    }
    100% {
      opacity: 1;
      transform: translateY(0px);
    }
  }
</style>

<div class="hero">
  <h1>Achchi Classical Dance Centre</h1>
  <p>Grace. Rhythm. Power. Welcome to your digital studio.</p>
  <button on:click={handleLogin}>Login</button>
</div>
