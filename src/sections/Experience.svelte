<script lang="ts">
  import type { Resume } from 'src/resume.schema';
  import { isPresent, formatDate } from '../utils';

  export let experience: Resume.IWork[];
</script>

<section>
  {#each experience as work}
    <p>
      <span><a href={work.url}>{work.name}</a> | {work.position}</span>
      
      <span
        >{#if work.startDate}
          {formatDate(work.startDate)} — {isPresent(work.endDate)
            ? 'Present'
            : formatDate(work.endDate)}
        {/if}

        {#if work.repo}
          <a href={work.repo}>(<strong>GitHub</strong>)</a>
        {/if}
      </span>
      
    </p>
    {#if work.highlights.length > 0}
      <ul>
        {#each work.highlights as highlight}
          <li>{@html highlight}</li>
        {/each}
        {#if work.technology && work.technology.length > 0}
          <li><strong>Technology:</strong> {work.technology.join(', ')}</li>
        {/if}
      </ul>
    {/if}
  {/each}
</section>

<style lang="scss">
  p {
    display: grid;
    grid-template-columns: repeat(2, max-content);
    justify-content: space-between;
    font-size: var(--title);

    &:not(:first-child) {
      margin-top: 0.75rem;
    }
  }

  a {
    font-family: var(--serif);
    font-weight: bold;
  }
</style>
