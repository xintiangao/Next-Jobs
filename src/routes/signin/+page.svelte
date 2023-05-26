<script>
  import Navbar from '../../Navbar.svelte';
  import { goto } from '$app/navigation';
  import { authenticateUser } from '../../utils/auth'; 

  let isLoading = false;

  async function signIn(evt) {
    evt.preventDefault();

    const userData = {
      username: evt.target['username'].value,
      password: evt.target['password'].value,
    };

    isLoading = true;

    const res = await authenticateUser(userData.username, userData.password);

    isLoading = false;

    if (res.success){
      goto('/');
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
    </div>

    <div class="form-control w-full">
      <label class="label" for="password">
        <span class="label-text">Password</span>
      </label>
      <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
    </div>

    <div class="form-control w-full mt-4">
      <div class="form-control w-full mt-4">
        <button class="btn btn-md" disabled={isLoading}>Log In</button>
      </div>
    </div>
  </form>
</div>