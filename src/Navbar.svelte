<script>
    import { authenticateUser, isAuthenticated, isLoggedIn, logOut } from "./utils/auth.js";
    let userLoggedIn = isLoggedIn;
    import { goto } from '$app/navigation';

    function goToSignInPage() {
        goto ('/signin')
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
        <li><a href="postjob">Post a Job</a></li>
    </ul>
    <ul>
        <li>{#if $isAuthenticated}<button on:click={logOut}>Sign Out</button>
            {:else}<a href="/signin" on:click={goToSignInPage}>Log In</a>{/if}</li>
    </ul>
</nav1>
  
