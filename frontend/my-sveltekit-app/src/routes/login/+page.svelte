<script>
  import { goto } from '$app/navigation';

  let username = '';
  let password = '';
  let error = '';

  function handleLogin() {
    if (username === 'danceacademy' && password === 'Dance@123') {
      goto('/dashboard');
    } else {
      error = '❌ Invalid credentials';
    }
  }
</script>

<style>
  .page {
    background: #1a1a1a;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 2rem;
    font-family: 'Segoe UI', sans-serif;
  }

  .card {
    background: #121212;
    border: 1px solid #333;
    border-radius: 12px;
    padding: 2.5rem;
    width: 100%;
    max-width: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.6);
    color: #f3f3f3;
  }

  h1 {
    text-align: center;
    font-size: 1.8rem;
    margin-bottom: 2rem;
    color: white;
  }

  label {
    display: block;
    margin-bottom: 0.5rem;
    font-size: 1rem;
    color: #ccc;
  }

  input {
    width: 100%;
    padding: 0.75rem 1rem;
    margin-bottom: 1.5rem;
    border: 1px solid #444;
    background-color: #1e1e1e;
    color: white;
    border-radius: 6px;
    font-size: 1rem;
    outline: none;
    transition: border-color 0.2s;
  }

  input:focus {
    border-color: #6366f1;
  }

  button {
    width: 100%;
    padding: 0.75rem;
    background-color: #6366f1;
    border: none;
    color: white;
    font-weight: bold;
    border-radius: 6px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.2s ease;
  }

  button:hover {
    background-color: #4f46e5;
  }

  .error {
    color: #f87171;
    text-align: center;
    margin-bottom: 1rem;
    font-size: 0.9rem;
  }
</style>

<div class="page">
  <div class="card">
    <h1>🕺 Dance Studio Login</h1>

    {#if error}
      <div class="error">{error}</div>
    {/if}

    <div>
      <label for="username">Username</label>
      <input id="username" type="text" bind:value={username} placeholder="Enter username" />
    </div>

    <div>
      <label for="password">Password</label>
      <input id="password" type="password" bind:value={password} placeholder="Enter password" />
    </div>

    <button on:click={handleLogin}>Login</button>
  </div>
</div>
