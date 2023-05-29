<script>
    import { isAuthenticated, logOut } from "./utils/auth.js";
    import { goto } from '$app/navigation';

    function goToSignInPage() {
        goto ('/signin')
    }
  
    function goToPostJobPage() {
        if ($isAuthenticated){
            goto('/postjob');
        }
        else {
            goto('/users/new');
        }
    }

</script>

<style>
  @import './utils/navbar.css';
</style>

<nav>
    <div class="next-jobs-db">
      <a href="/">
        <button>NEXT Jobs DB</button>
      </a>
    </div>
  </nav>
  
<nav1>
    <ul>
        <button on:click={goToPostJobPage}>Post a Job</button>
    </ul>
    <ul>
        {#if $isAuthenticated}
            <button on:click={logOut}>Sign Out</button>
        {:else}
            <a href="/signin" on:click={goToSignInPage}>Log In</a>{/if}
    </ul>
</nav1>
  