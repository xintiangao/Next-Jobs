<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { getUserId } from '../../utils/auth';

    function generateJobDataID() {
        const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
        let result = '';

        for (let i = 0; i < 15; i++) {
            const randomIndex = Math.floor(Math.random() * characters.length);
            result += characters.charAt(randomIndex);
        }
        return result;
    }

    async function postJob(evt) {
        evt.preventDefault()
        
        const jobData = {

            // user: getUserId(),
            // id: generateJobDataID(),
            // title: 'test',
            // minAnnualCompensation: '300000',
            // maxAnnualCompensation: '500000',
            // employer: 'testtesttesttest',
            // location: 'testtesttesttest',
            // description: 'testtesttesttest',
            // requirements: 'testtesttesttest',
            // applicationInstructions: 'testtesttesttest',

            user: getUserId(),
            id: generateJobDataID(),
            title: evt.target['title'].value,
            minAnnualCompensation: evt.target['minAnnualCompensation'].value,
            maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
            employer: evt.target['employer'].value,
            location: evt.target['location'].value,
            description: evt.target['description'].value,
            requirements: evt.target['requirements'].value,
            applicationInstructions: evt.target['applicationInstruction'].value,
        };

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
            
        <div class="form-control w-full mt-4">
            <button type="submit" class="btn btn-md">Submit</button>
        </div>

        <div class="form-control w-full mt-8">
        </div>
</form>


