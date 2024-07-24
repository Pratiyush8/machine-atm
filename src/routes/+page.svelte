<script>
    import { auth } from '../db/firebase';
    import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword } from 'firebase/auth';
  
    let email = '';
    let password = '';
    let isNewUser = false;
    let errorMessage = '';
  
    async function handleAuth() {
      try {
        if (isNewUser) {
          await createUserWithEmailAndPassword(auth, email, password);
        } else {
          await signInWithEmailAndPassword(auth, email, password);
        }
      } catch (error) {
        errorMessage = error.message;
      }
    }
  </script>
  
  <form on:submit|preventDefault={handleAuth}>
    <input type="email" bind:value={email} placeholder="Email" required />
    <input type="password" bind:value={password} placeholder="Password" required />
    <button type="submit">{isNewUser ? 'Sign Up' : 'Login'}</button>
    <p>{errorMessage}</p>
    <button type="button" on:click={() => isNewUser = !isNewUser}>
      {isNewUser ? 'Switch to Login' : 'Switch to Sign Up'}
    </button>
  </form>
  
