<script>

let userLoggedIn = false;
import { authenticateUser, logOut } from "./utils/auth.js";

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
      <li>{#if userLoggedIn}<button on:click={logOut}>Sign Out</button>{:else}<a href="/signin" on:click={authenticateUser}>Log In</a>{/if}</li>
    </ul>
  </nav1>
  
