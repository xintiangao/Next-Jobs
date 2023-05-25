<script>
    import Navbar from '../../Navbar.svelte';
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
const jobData = {
  'Job Title': "",
  'Min Annual Compensation': "",
  'Max Annual Compensation': "",
  'Company Name': "",
  'Description' :"",
  'Requirements':"",
  'Application-Instruction':"",
}

async function postJob() {
  try {
    const response = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': getTokenFromLocalStorage()
      },
      body: JSON.stringify(jobData)
    });

    if (response.status === 200) {
      alert ('successful')
    } else {
      console.error('Failed to post the job:', response.status, response.statusText);
    }
  } catch (error) {
    console.error('An error occurred while posting the job:', error);
  }
}
</script>

<Navbar />
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
            <label class ="label" for = "description">
                <span class ="label-text">Description</span>
            </label>
            <textarea class = "textarea textarea-bordered h-64" name = "description" placeholder></textarea>
        </div>

        <div class ="form-control">
            <label class ="label" for = "requirements">
                <span class ="label-text">Requirements</span>
            </label>
            <textarea class = "textarea textarea-bordered h-64" name = "description" placeholder></textarea>
        </div>

        <div class ="form-control">
            <label class ="label" for = "application-instruction">
                <span class ="label-text">Application-Instruction</span>
            </label>
            <textarea class = "textarea textarea-bordered h-24" name = "description" placeholder></textarea>
        </div>

        <div class="form-control w-full mt-8">
            <button class="btn btn-md" on:click={postJob}>
              <div class="hidden" role="status"></div>
              Post Job
            </button>
        </div>
          
        <div class = "mt-28"></div>
    </div>

