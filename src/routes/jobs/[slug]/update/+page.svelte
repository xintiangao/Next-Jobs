<script>
    import Navbar from '../../../../Navbar.svelte';
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { getTokenFromLocalStorage, getUserId } from '../../../../utils/auth';

    export let data

    let title= data.job.title;
    let minAnnualCompensation= data.job.minAnnualCompensation;
    let maxAnnualCompensation= data.job.maxAnnualCompensation;
    let employer= data.job.employer;
    let location= data.job.location;
    let description= data.job.description;
    let requirements= data.job.requirements;
    let applicationInstructions= data.job.applicationInstructions;


    async function updateJob(evt) {
        evt.preventDefault()
        
        const jobData = {

            user: getUserId(),
            id: data.job.id,
            title: evt.target['title'].value,
            minAnnualCompensation: evt.target['minAnnualCompensation'].value,
            maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
            employer: evt.target['employer'].value,
            location: evt.target['location'].value,
            description: evt.target['description'].value,
            requirements: evt.target['requirements'].value,
            applicationInstructions: evt.target['applicationInstruction'].value,

            // user: getUserId(),
            // id: generateJobDataID(),
            // title: evt.target['title'].value,
            // minAnnualCompensation: evt.target['minAnnualCompensation'].value,
            // maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
            // employer: evt.target['employer'].value,
            // location: evt.target['location'].value,
            // description: evt.target['description'].value,
            // requirements: evt.target['requirements'].value,
            // applicationInstructions: evt.target['applicationInstruction'].value,
        };

    const response = await fetch(PUBLIC_BACKEND_BASE_URL + `/api/collections/jobs/records/${jobData.id}`, {
        method: 'PATCH',
        mode:'cors',
        headers: {
            'Content-Type': 'application/json',
            Authorization: getTokenFromLocalStorage()
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
<form on:submit={updateJob} class="w-full">
    <div class = "container mx-auto px-2 lg:px-0">
        <div class = "form-control w-full">
            <label class = "label" for="title"></label> 
                <span class = "label-text">Job Title</span>
                <input type ="text" name = "title" class = "input input-bordered w-full" bind:value={title} required>
        </div>

        <div class = "form-control w-full">
            <label class = "label" for="title"><span class = "label-text">Min Annual Compensation</span></label> 
                <input type ="number" name = "minAnnualCompensation" class = "input input-bordered w-full" bind:value={minAnnualCompensation} required>
                <label class = "label" for = "salary">
                    <span class = "label-text-alt">USD</span>
                    <span class = "label-tet-alt">per annum</span>
                </label>
        </div>

        <div class = "form-control w-full">
            <label class = "label" for="title"><span class = "label-text">Max Annual Compensation</span></label> 
                <input type ="number" name = "maxAnnualCompensation" class = "input input-bordered w-full" bind:value={maxAnnualCompensation} required>
                <label class = "label" for = "salary">
                    <span class = "label-text-alt">USD</span>
                    <span class = "label-tet-alt">per annum</span>
                </label>
        </div>

        <div class ="form-control w-full">
            <label class ="label" for = "salary">
                <span class ="label-text">Company Name</span>
            </label>
            <input type = "text" name = "employer" class = "input input-bordered w-full" bind:value={employer} required>
        </div>

        <div class ="form-control w-full">
            <label class ="label" for = "salary">
                <span class ="label-text">Job Location</span>
            </label>
            <input type = "text" name = "location" class = "input input-bordered w-full" bind:value={location} required>
        </div>

        <div class ="form-control w-full">
            <label class ="label" for = "description">
                <span class ="label-text">Description</span>
            </label>
            <textarea class = "textarea textarea-bordered h-64" name = "description" bind:value={description} required></textarea>
        </div>

        <div class ="form-control">
            <label class ="label" for = "requirements">
                <span class ="label-text">Requirements</span>
            </label>
            <textarea class = "textarea textarea-bordered h-64" name = "requirements" bind:value={requirements} required></textarea>
        </div>

        <div class ="form-control">
            <label class ="label" for = "application-instruction">
                <span class ="label-text">Application-Instruction</span>
            </label>
            <textarea class = "textarea textarea-bordered h-24" name = "applicationInstruction" bind:value={applicationInstructions} required></textarea>
        </div>
            
        <div class="form-control w-full mt-4">
            <button type="submit" class="btn btn-md">Update</button>
        </div>

        <div class="form-control w-full mt-8">
        </div>
</form>


