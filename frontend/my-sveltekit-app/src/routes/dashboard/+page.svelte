<script>
  let selectedFilter = 'all';
  let view = 'current';
let totalAmount = 1000; // ₹1000 per student per month (you can adjust)


$: totalStudents = students.length;
$: paidCount = students.filter(s => s.paid).length;
$: unpaidCount = totalStudents - paidCount;
$: totalCollected = paidCount * totalAmount;


  let students = [
    { name: 'Anita Sharma', paid: true, history: { Jan: true, Feb: true, Mar: false } },
    { name: 'Rahul Verma', paid: false, history: { Jan: true, Feb: false, Mar: false } },
    { name: 'Meena Iyer', paid: true, history: { Jan: true, Feb: true, Mar: true } },
    { name: 'Ravi Kumar', paid: false, history: { Jan: false, Feb: false, Mar: false } }
  ];


import { goto } from '$app/navigation';

function handleLogout() {
  goto('/');
}

  const months = ['Jan', 'Feb', 'Mar'];

  function sendReminder(student) {
    alert(`Reminder sent to ${student.name}`);
  }

  function sendPaymentLink(student) {
    alert(`Payment link sent to ${student.name}`);
  }

  $: filteredStudents = students.filter(s =>
    selectedFilter === 'all' ? true : selectedFilter === 'paid' ? s.paid : !s.paid
  );
</script>

<style>
  html, body {
    margin: 0;
    padding: 0;
    background-color: #1a1a1a;
    color: #f3f3f3;
    font-family: 'Segoe UI', sans-serif;
    overflow-x: hidden;
  }

  .container {
    width: 100%;
    max-width: 1080px;
    margin: 2rem auto;
    padding: 1rem 1.5rem;
    box-sizing: border-box;
    background: #121212;
    border-radius: 12px;
    border: 1px solid #333;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
  }

  h2 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 1.5rem;
  }

  .controls {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  .view-buttons button {
    padding: 0.6rem 1rem;
    font-size: 1rem;
    font-weight: 600;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    background-color: #2e2e2e;
    color: #f3f3f3;
    transition: background-color 0.2s ease;
  }

  .view-buttons button.active {
    background-color: #6366f1;
  }

  .filter select {
    padding: 0.5rem 1rem;
    background: #1e1e1e;
    color: white;
    border: 1px solid #444;
    border-radius: 6px;
    font-size: 1rem;
  }

  .logout-bar {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1rem;
    flex-wrap: wrap;
  }

  .logout-bar button {
    background-color: #f87171;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.2s ease;
  }

  .logout-bar button:hover {
    background-color: #ef4444;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 1rem;
    overflow-x: auto;
  }

  th, td {
    padding: 0.75rem;
    text-align: left;
    border-bottom: 1px solid #333;
    white-space: nowrap;
  }

  th {
    background-color: #1f1f1f;
    color: #aaa;
    font-size: 0.95rem;
  }

  td {
    font-size: 0.95rem;
  }

  .paid {
    color: #4ade80;
    font-weight: 600;
  }

  .unpaid {
    color: #f87171;
    font-weight: 600;
  }

  .actions button {
    padding: 0.4rem 0.7rem;
    margin-right: 0.4rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.85rem;
    transition: background-color 0.2s ease;
  }

  .reminder-btn {
    background-color: #facc15;
    color: #111;
  }

  .reminder-btn:hover {
    background-color: #eab308;
  }

  .link-btn {
    background-color: #6366f1;
    color: white;
  }

  .link-btn:hover {
    background-color: #4f46e5;
  }

  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
    margin-top: 2rem;
  }

  .stat-card {
    background-color: #1f1f1f;
    border: 1px solid #333;
    padding: 1.2rem;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
    text-align: center;
  }

  .stat-card h3 {
    font-size: 1rem;
    margin-bottom: 0.5rem;
    color: #ccc;
  }

  .stat-card p {
    font-size: 1.7rem;
    font-weight: bold;
  }

  .stat-card.green p { color: #4ade80; }
  .stat-card.red p { color: #f87171; }
  .stat-card.indigo p { color: #a78bfa; }
  .stat-card.blue p { color: #60a5fa; }

  @media (max-width: 640px) {
    h2 {
      font-size: 1.5rem;
    }

    .controls {
      flex-direction: column;
      align-items: flex-start;
    }

    th, td {
      font-size: 0.85rem;
    }

    .view-buttons button,
    .filter select,
    .logout-bar button {
      font-size: 0.9rem;
      padding: 0.5rem 0.8rem;
    }

    .actions button {
      font-size: 0.75rem;
      padding: 0.3rem 0.6rem;
    }

    .card-grid {
      grid-template-columns: 1fr 1fr;
    }
  }
</style>



<div class="container">
<div class="logout-bar">
  <button on:click={handleLogout}>🚪 Logout</button>
</div>

  <h2>💼 Payment Management Dashboard</h2>

  <div class="controls">
    <div class="view-buttons">
  <button class:active={view === 'current'} on:click={() => view = 'current'}>🔄 Current Month</button>
  <button class:active={view === 'history'} on:click={() => view = 'history'}>📅 History View</button>
  <button class:active={view === 'summary'} on:click={() => view = 'summary'}>📦 Summary Cards</button>
</div>


    {#if view === 'current'}
      <div class="filter">
        <label>Filter:</label>
        <select bind:value={selectedFilter}>
          <option value="all">All</option>
          <option value="paid">Paid</option>
          <option value="unpaid">Unpaid</option>
        </select>
      </div>
    {/if}
  </div>

  {#if view === 'current'}
    <table>
      <thead>
        <tr>
          <th>Student Name</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        {#each filteredStudents as student}
          <tr>
            <td>{student.name}</td>
            <td class={student.paid ? 'paid' : 'unpaid'}>
              {student.paid ? '✅ Paid' : '❌ Unpaid'}
            </td>
            <td class="actions">
              {#if !student.paid}
                <button class="reminder-btn" on:click={() => sendReminder(student)}>Send Reminder</button>
                <button class="link-btn" on:click={() => sendPaymentLink(student)}>Send Link</button>
              {/if}
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  {:else if view === 'history'}
    <table>
      <thead>
        <tr>
          <th>Student Name</th>
          {#each months as month}
            <th>{month}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each students as student}
          <tr>
            <td>{student.name}</td>
            {#each months as month}
              <td class={student.history[month] ? 'paid' : 'unpaid'}>
                {student.history[month] ? '✅' : '❌'}
              </td>
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>

    {:else if view === 'summary'}
  <div class="card-grid">
    <div class="card stat-card green">
      <h3>Paid Students</h3>
      <p>{paidCount}</p>
    </div>
    <div class="card stat-card red">
      <h3>Unpaid Students</h3>
      <p>{unpaidCount}</p>
    </div>
    <div class="card stat-card indigo">
      <h3>Total Students</h3>
      <p>{totalStudents}</p>
    </div>
    <div class="card stat-card blue">
      <h3>Total Collected</h3>
      <p>₹{totalCollected}</p>
    </div>
  </div>

  {/if}
</div>
