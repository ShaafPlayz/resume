<script lang="ts">
  import type { Resume } from 'src/resume.schema';

  export let basics: Resume.IBasics;
</script>

<section>
  <h1>{basics.name}</h1>
  <div class="contacts">
    <div class="contact">
      <i class="fas fa-inbox" />
      <a href="mailto:{basics.email}">{basics.email}</a>
    </div>
    <div class="lower">
      <div class="contact">
        <i class="fas fa-link" />
        <a href={basics.url}>{basics.url.replace('https://', '')}</a>
      </div>
      {#each basics.profiles as profile}
        <div class="contact">
          <i class="fab fa-{profile.network}" />
          <a href={profile.url}>{profile.username}</a>
        </div>
      {/each}
    </div>
  </div>
</section>

<style lang="scss">
  section {
    display: grid;
    grid-template-columns: auto 19rem;
    height: max-content;
  }

  h1 {
    font-family: var(--serif);
    font-size: #{calc(28pt / 13pt)}rem;
  }

  .contacts {
    display: grid;
    row-gap: 0.25rem;
    font-size: var(--normal);
  }

  .contact {
    display: grid;
    grid-template-columns: 1rem auto;
    column-gap: 0.1rem;
    align-items: center;
  }

  i {
    transform: translateY(1px);
    color: var(--gray);
  }

  .lower {
    display: grid;
    grid-template-columns: 1fr 1.5fr 1fr;

    & .contact:nth-child(2) {
      justify-content: center;
    }

    & .contact:nth-child(3) {
      justify-content: right;
    }
  }
</style>
