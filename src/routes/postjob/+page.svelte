<script>
    import Navbar from '../../Navbar.svelte';
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { getTokenFromLocalStorage } from '../../utils/auth';
    // import PocketBase from 'pocketbase';

    // const pb = new PocketBase('http://127.0.0.1:5173');

    async function postPostJOb() {
        goto('/');
    }

    
    async function postJob(evt) {
        evt.preventDefault()

        const jobData = {
            
            // "collectionId": "t9mzd3reuf1yxpg",
            // "collectionName": "jobs",
            // "created": "2022-01-01 01:00:00.123Z",
            // "updated": "2022-01-01 23:59:59.456Z",

            "user": 'userID',
            "title": "test",
            "minAnnualCompensation": 123,
            "maxAnnualCompensation": 123,
            "description": "test",
            "requirements": "test",
            "applicationInstructions": "test",
            "location": "test",
            "employer": "test"

        } ;
        // const jobData = {
        //     title: evt.target['title'].value,
        //     minAnnualCompensation: evt.target['minAnnualCompensation'].value,
        //     maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
        //     companyName: evt.target['employer'].value,
        //     jobLocation: evt.target['location'].value,
        //     description: evt.target['description'].value,
        //     requirements: evt.target['requirements'].value,
        //     applicationInstructions: evt.target['applicationInstruction'].value,
        // } ;

        console.log(jobData)

    try {

        const response = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
            'Content-Type': 'application/json',
            // 'Authorization': getTokenFromLocalStorage()
        },
        body: JSON.stringify(jobData)
        });

        if (response.status === 200) {
        alert ('successful');
        postPostJOb();
        } else {
            console.error(response.Text);
        }
    } catch (error) {
        console.error('An error occurred while posting the job:', error);
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
            <button type="submit" class="btn btn-md">
              Post Job
            </button>
          </div>
          
        <div class = "mt-28"></div>
    </div>
    </form>

