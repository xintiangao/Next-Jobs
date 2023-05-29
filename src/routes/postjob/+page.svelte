<script>
    import Navbar from '../../Navbar.svelte';
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { getUserId } from '../../utils/auth';

    let isLoading = false;

    async function postJob(evt) {
        evt.preventDefault()
        
        const jobData = {
            user: getUserId(),
            title: evt.target['title'].value,
            minAnnualCompensation: evt.target['minAnnualCompensation'].value,
            maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
            employer: evt.target['employer'].value,
            location: evt.target['location'].value,
            description: evt.target['description'].value,
            requirements: evt.target['requirements'].value,
            applicationInstructions: evt.target['applicationInstruction'].value,
        };
        
        let isLoading = true;

        const response = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(jobData)
        });

        if (response.status == 200) {
        goto (`/jobs/${jobData.id}`)
        } else {
            console.error('Failed to create record:', error);
        }
}

</script>

<Navbar />
<form on:submit={postJob} class="w-full">
    <div class = "container mx-auto px-2 lg:px-0">
        <div class = "form-control w-full">
            <label class = "label" for="title"></label> 
                <span class = "label-text">Job Title</span>
                <input type ="text" name = "title" placeholder="Software Engineer" class = "input input-bordered w-full">
        </div>

        <div class = "form-control w-full">
            <label class = "label" for="title"><span class = "label-text">Min Annual Compensation</span></label> 
                <input type ="number" name = "minAnnualCompensation" placeholder="40,000" class = "input input-bordered w-full">
                <label class = "label" for = "salary">
                    <span class = "label-text-alt">USD</span>
                    <span class = "label-tet-alt">per annum</span>
                </label>
        </div>

        <div class = "form-control w-full">
            <label class = "label" for="title"><span class = "label-text">Max Annual Compensation</span></label> 
                <input type ="number" name = "maxAnnualCompensation" placeholder="250,000" class = "input input-bordered w-full">
                <label class = "label" for = "salary">
                    <span class = "label-text-alt">USD</span>
                    <span class = "label-tet-alt">per annum</span>
                </label>
        </div>

        <div class ="form-control w-full">
            <label class ="label" for = "salary">
                <span class ="label-text">Company Name</span>
            </label>
            <input type = "text" name = "employer" placeholder="e.g. Facebook" class = "input input-bordered w-full">
        </div>

        <div class ="form-control w-full">
            <label class ="label" for = "salary">
                <span class ="label-text">Job Location</span>
            </label>
            <input type = "text" name = "location" placeholder="e.g. Singapore" class = "input input-bordered w-full">
        </div>

        <div class ="form-control w-full">
            <label class ="label" for = "description">
                <span class ="label-text">Description</span>
            </label>
            <textarea class = "textarea textarea-bordered h-64" name = "description" placeholder></textarea>
        </div>

        <div class ="form-control">
            <label class ="label" for = "requirements">
                <span class ="label-text">Requirements</span>
            </label>
            <textarea class = "textarea textarea-bordered h-64" name = "requirements" placeholder></textarea>
        </div>

        <div class ="form-control">
            <label class ="label" for = "application-instruction">
                <span class ="label-text">Application-Instruction</span>
            </label>
            <textarea class = "textarea textarea-bordered h-24" name = "applicationInstruction" placeholder></textarea>
        </div>
            
        <div class="form-control w-full mt-8">
            <div class="form-control w-full mt-4">
              {#if isLoading}
              <div class="flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="animate-spin -ml-1 mr-3 h-5 w-5 text-gray-700">
                  <circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="4" />
                  <path fill="currentColor" d="M12 2v4m0 12v4m-4-4H2M18 2h4" />
                </svg>
                <span class="text-lg text-gray-700">Loading...</span>
              </div>
              {:else}
              <button type="submit" class="btn btn-md">Submit</button>
              {/if}
            </div>
        </div>
    </div>
</form>


