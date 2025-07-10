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
    return value !== null ? `${value}%` : ''
  }
</script>

<h1>Book calculator</h1>
<input type="number" bind:value={pageStart} placeholder="Pagina de inicio" />
<input type="number" bind:value={pageEnd} placeholder="Pagina de fin" />
<br />
<input type="number" bind:value={pageCurrent} placeholder="Pagina actual" />
<br />
<input type="text" disabled bind:value={pageProgress} placeholder="Progreso" />
