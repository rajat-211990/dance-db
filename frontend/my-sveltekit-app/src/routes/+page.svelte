<script>
  let selectedFilter = 'all';

  let students = [
    { name: 'Anita Sharma', paid: true },
    { name: 'Rahul Verma', paid: false },
    { name: 'Meena Iyer', paid: true },
    { name: 'Ravi Kumar', paid: false }
  ];

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
  body {
    background-color: #1a1a1a;
    color: #f3f3f3;
    font-family: 'Segoe UI', sans-serif;
  }

  .container {
    max-width: 960px;
    margin: 3rem auto;
    padding: 1rem 2rem;
    background: #121212;
    border-radius: 12px;
    border: 1px solid #333;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
  }

  h2 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 2rem;
    color: white;
  }

  .filter {
    margin-bottom: 1.5rem;
    text-align: right;
  }

  .filter label {
    margin-right: 0.5rem;
    font-size: 1rem;
    color: #ccc;
  }

  select {
    padding: 0.5rem 1rem;
    border-radius: 6px;
    background: #1e1e1e;
    color: white;
    border: 1px solid #444;
    font-size: 1rem;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 1rem;
  }

  th, td {
    padding: 1rem;
    text-align: left;
    border-bottom: 1px solid #333;
  }

  th {
    background-color: #1f1f1f;
    color: #aaa;
    font-weight: 600;
  }

  td {
    font-size: 1rem;
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
    padding: 0.4rem 0.75rem;
    margin-right: 0.5rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.9rem;
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
</style>

<div class="container">
  <h2>📊 Monthly Payments Dashboard</h2>

  <div class="filter">
    <label for="filter">Filter:</label>
    <select id="filter" bind:value={selectedFilter}>
      <option value="all">All</option>
      <option value="paid">Paid</option>
      <option value="unpaid">Unpaid</option>
    </select>
  </div>

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
</div>
