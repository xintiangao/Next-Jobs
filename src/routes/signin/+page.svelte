<script>
  import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
  let formErrors = {};
  import Navbar from '../../Navbar.svelte';
  import { goto } from '$app/navigation';
  import { isLoggedIn } from '../../utils/auth';
  import { authenticateUser } from '../../utils/auth'; 

  async function signIn() {
    try {
      const rawResp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/users/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          identity: username,
          password 
        })
      });

      let resp = await JSON(rawResp);

      if (resp.status === 200) {
        goto('/postjob');
        isLoggedIn();
      } else {
        const errorData = await resp.json();
        console.error('Sign in error:', errorData);
      }
    } catch (error) {
      alert ('Error occurred during sign in');
    }
  }
</script>

<Navbar />

<h1 class="text-center text-xl">Log In</h1>
<div class="text-center">
  <a class="link-hover italic text-xs" href="/users/new">Don't have an account? Click here to Sign Up instead.</a>
</div>
<div class="flex justify-center items-center mt-8">
  <form on:submit={signIn} class="w-1/3">
    <div class="form-control w-full">
      <label class="label" for="username">
        <span class="label-text">Username</span>
      </label>
      <input type="text" name="username" placeholder="johndoe" class="input input-bordered w-full" />
      {#if 'username' in formErrors}
      <label class="label" for="username">
        <span class="label-text-alt text-red-500">{formErrors['username'].message}</span>
      </label>
      {/if}
    </div>

    <div class="form-control w-full">
      <label class="label" for="password">
        <span class="label-text">Password</span>
      </label>
      <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
      {#if 'password' in formErrors}
      <label class="label" for="password">
        <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
      </label>
      {/if}
    </div>

    <div class="form-control w-full mt-4">
      <div class="form-control w-full mt-4">
        <button class="btn btn-md" on:submit={() => authenticateUser}>Log In</button>
      </div>
    </div>
  </form>
</div>
