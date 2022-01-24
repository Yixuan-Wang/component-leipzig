<svelte:options tag="leipzig-gloss"/>
<script>
  export let def = '.:#';
  export let data;
  export let lang = '';

  function parse(str) {
    if (!str) {
      return {
        maxLength: 0,
        lines: [],
      };
    }
    const lines = str.trim().split(/\n\s*/).map((line, index) => {
      line = line.trim()
      return def[index] === '#' ? [line] : line.split(' ')
    })
    return {
        maxLength: Math.max(...lines.map(line => line.length)),
        lines,
      };
  }

  function splitGloss(str) {
    const parts = str.split(/([\-\.=_;:\\>~\[\]\(\)<>])/)
    return parts.map(part => {
      if ('-.=_;:\\>~[]()<>'.includes(part)) return { value: part }
      if (part.match(/^\d?[A-Z]+$/)) return { label: true, value: part }
      else return { value: part }
    })
  }

  let leipzig;
  let langs;
  leipzig = parse(data);
  langs = lang.split(',');
</script>

<div class="leipzig-container">
  <div class="leipzig">
    {#each leipzig.lines as lines, lineNum}
      {#each lines as token}
        {#if def[lineNum] === '#'}
          <span lang={langs[lineNum] ?? ''} style:grid-row-start={`${lineNum+1}`} style:grid-column={`1/span ${leipzig.maxLength}`}>{token}</span>
        {:else if def[lineNum] === ':'}
          <span lang={langs[lineNum] ?? ''} style:grid-row-start={`${lineNum+1}`}>
            {#each splitGloss(token) as gloss}
              <span style:font-variant-caps={gloss.label ? 'all-small-caps' : 'initial'}>{gloss.value}</span>
            {/each}
          </span>
        {:else}
          <span lang={langs[lineNum] ?? ''} style:grid-row-start={`${lineNum+1}`}>{token}</span>
        {/if}
      {/each}
    {/each}
  </div>
</div>

<style>
  .leipzig {
    display: grid;
    column-gap: 1em;
    overflow-x: auto;
    justify-content: start;
    justify-items: left;
  }
</style>
