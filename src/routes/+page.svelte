<script>
  import humanize from 'humanize-plus';
  export let data;
  import Navbar from '../Navbar.svelte';
</script>


<div>
  <Navbar />
  
  <h1 class="text-primary text-center text-xl font-bold">Find Your Next Job</h1>
  
  <div class="text-primary overflow-x-auto w-full">
    {#each data.jobs as job}
    <div class="flex flex-col mt-10 ml-20 mr-20">
      <div>
        <a class="font-bold text-2xl" href="/jobs/{job.id}">{job.title}</a>
        <div class="text-sm mt-1">
          {job.employer} . {job.location} .
          <span class="text-sm">USD {humanize.formatNumber(job.minAnnualCompensation
          )} - USD {humanize.formatNumber(
            job.maxAnnualCompensation
            )}</span>
                </div>
                <div class="italic text-xs opacity-50 mt-2">
                  posted {new Date(job.created).toLocaleDateString(undefined, {
                    weekday: 'long',
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric'
                  })}
              </div>
            </div>

            <div class="mt-4 ">
                {job.description.slice(0, 240)}...
            </div>
        </div>
    {/each}
  </div>
</div>
