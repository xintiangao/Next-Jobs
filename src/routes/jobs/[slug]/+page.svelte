<script>
    import humanize from "humanize-plus";
    import SvelteMarkdown from 'svelte-markdown';
    export let data;
    import Navbar from "../../../Navbar.svelte";
	import { getUserId } from "../../../utils/auth";
</script>
  <Navbar />

  <div class="text-primary mt-10 ml-20">
    <div class="flex">
      <div class="flex-1">
        <h1 class="text-3xl font-extrabold">{data.job.title}</h1>
        <p class="text-xl">{data.job.employer}</p>
      </div>
      <div class="flex-none mr-10">
        {#if getUserId() === data.job.user}
        <a href="/jobs/{data.job.id}/update" class="btn btn-ghost font-medium">EDIT</a>
        {/if}
      </div>
    </div>
  
    <div class="flex flex-row w-full mt-8">
      <div class="basis-2/3 prose max-w-none w-full text-primary">
        <h2 class="text-xl font-thin text-primary">Description</h2>
        <SvelteMarkdown source={data.job.description} />
        <div>
          {data.job.description}
        </div>
        <div class="mt-6" />
        <h2 class="text-xl font-thin text-primary">Requirements</h2>
        <SvelteMarkdown source={data.job.requirements} />
        <div>
          {data.job.requirements}
          <div />
          <div class="mt-6" />
          <h2 class="text-xl font-thin text-primary">How to Apply?</h2>
          <p>{data.job.applicationInstructions}</p>
        </div>
        <div class="basis-1/3">
          <h2 class="text-xl font-thin text-primary">Location</h2>
          <p>{data.job.location}</p>
          <div class="mt-6" />
          <h2 class="text-xl font-thin text-primary">Salary Range</h2>
          <p>
            USD {humanize.formatNumber(data.job.minAnnualCompensation)} - USD
            {humanize.formatNumber( data.job.maxAnnualCompensation )}
          </p>
        </div>
      </div>
    </div>
  </div>