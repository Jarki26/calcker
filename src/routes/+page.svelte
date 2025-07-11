<script lang="ts">
  let pageStart: number | null = $state(null)
  let pageEnd: number | null = $state(null)
  let pageCurrent: number | null = $state(null)
  let pageProgress: string = $derived(
    formatNumberPercentage(calculateProgress(pageStart, pageEnd, pageCurrent))
  )

  function calculateProgress(
    pageStart: number | null,
    pageEnd: number | null,
    pageCurrent: number | null
  ) {
    console.log(
      `Calculating progress with start: ${pageStart}, end: ${pageEnd}, current: ${pageCurrent}`
    )
    if (
      pageStart !== null &&
      pageEnd !== null &&
      pageEnd > 0 &&
      pageCurrent !== null &&
      pageCurrent != 0 &&
      pageCurrent >= pageStart
    ) {
      const totalPages = pageEnd - pageStart + 1
      const currentPageIndex = pageCurrent - pageStart + 1
      return Math.round((currentPageIndex / totalPages) * 100)
    } else if (pageStart !== null && pageEnd !== null) {
      return Math.round((pageStart / pageEnd) * 100)
    } else {
      return null
    }
  }

  function formatNumberPercentage(value: number | null): string {
    return value !== null ? `${value}%` : ""
  }
</script>

<div class="container">
  <h1 class="library-title">Book calculator</h1>
  <div class="book-form">
    <div class="page">
      <input
        type="number"
        bind:value={pageStart}
        placeholder="Pagina de inicio"
      />
      <input type="number" bind:value={pageEnd} placeholder="Pagina de fin" />
    </div>
    <div class="separator"></div>
    <!-- Separator updated -->
    <div class="page">
      <input
        type="number"
        bind:value={pageCurrent}
        placeholder="Pagina actual"
      />
      <input
        type="text"
        disabled
        bind:value={pageProgress}
        placeholder="Progreso"
      />
    </div>
  </div>
</div>

<style>
  .container {
    background-color: #fffbd2;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    padding-left: 1rem;
    padding-right: 1rem;
  }
  .library-title {
    font-family: "Georgia", serif;
    font-size: 2.5rem;
    text-align: center;
    color: #4a4a4a;
    margin-bottom: 1rem;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
  }

  .book-form {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    border: 4px solid #b22222; /* Red border resembling a book cover */
    padding: 1rem;
    border-radius: 12px; /* Slightly rounded corners for a book-like appearance */
    background-color: #f9f9f9;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    flex-wrap: wrap; /* Adjust layout for smaller screens */
  }

  .page {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    width: 100%; /* Ensure pages take full width on small screens */
    max-width: 300px; /* Limit width for larger screens */
  }

  .separator {
    background-color: #b22222; /* Match the book cover border color */
    margin: 1rem 0; /* Add spacing around the separator */
    width: 2px; /* Default vertical separator */
    height: auto;
  }

  @media (max-width: 600px) {
    .separator {
      width: 100%; /* Horizontal separator for mobile view */
      height: 2px;
    }
  }

  input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 1rem;
  }

  input:disabled {
    background-color: #e9e9e9;
    color: #666;
  }

  @media (max-width: 600px) {
    .book-form {
      gap: 1rem; /* Reduce gap for smaller screens */
      padding: 0.5rem; /* Adjust padding for mobile */
    }

    .page {
      max-width: 100%; /* Ensure pages take full width on very small screens */
    }

    input {
      font-size: 0.9rem; /* Adjust font size for smaller screens */
    }
  }
</style>
