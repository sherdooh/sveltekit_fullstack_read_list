<script>
  import { authHandlers } from "../store/store";

    let email="";
    let password="";
    let confirmPass="";
    let error = false;
    let register = false;
    let authenticating = false;

    async function handleAuthenticate() {
        if (!email || !password || (register && !confirmPass)){
            error = true;
            return;
        }

        try {
            if(!register) {
            authHandlers.login(emial,password);
        } else {
            await authHandlers.login(email, password);
        }
            
        } catch (err) {
            console.log("Authetication error!!", err);
            error = true;
            
        }


    }
    function handleRegister() {
        register = !register;
    }
</script>


<div class="authContainer">
    <form>
        <h1>{register ? "Register" : "Login"}</h1>
        {#if error}
        <p class="error"> Information provided incorrect</p>
        {/if}
        
        <label>
            <p class={email ? 'above' : 'center'}>Email</p>
            <input
                bind:value={email} 
                type="email" 
                placeholder="Email" 
            />
        </label>

        <label>
            <p class={email ? 'above' : 'center'}>Password</p>
            <input 
                bind:value={password}
                type="password" 
                placeholder="Password" 
            />
        </label>
            {#if register}

            <label>
                <p class={email ? 'above' : 'center'}>Confirm Password</p>
                <input 
                    bind:value={confirmPass}
                    type="password" 
                    placeholder="Confirm Password" 
                />
            </label>

                
            {/if}
        
        <button type="buttom">Submit</button>
    </form>

    <div class="preference">
        <p>Or</p>
        {#if register}
            <p>Already have an account?</p>
            <p class="auth" on:click={handleRegister} on:keydown={() =>{}}>Login</p>
        {:else}
            <p>Don't have an account?</p>
            <p class="auth" on:click={handleRegister} on:keydown={() =>{}} 
            >Register</p>
        {/if}
    </div>

</div>
<style>
    .authContainer {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); 
    }
    
    form{
        display: flex;
        flex-direction: column;
        gap: 8px;
        width: 400px;
        max-width: 100%;
        margin: 0 auto;
        
    }
    form input{
        width: 100%;
        background: transparent;
        color: white;
        padding: 8px 14px;

    }
    form h1 {
        text-align: center;
        font-size: 3rems;
        font-variant: normal;
        
    }
    form label{
        position: relative;
        border: 3px solid navy;
        border-radius: 5px;
    }

    form input:focus{
        border: none;
        outline: none;

    }
    form button {
        background-color: #002212;
        color: white;
        border: none;
        padding: 10px;
        cursor: pointer;
        border-radius: 5px;
    }
    form button:hover{
        background-color: blue;
    }
    .above, .center{
        position: absolute;
        transform: translateY(-50%);
        pointer-events: none;
        color: white;
        border-radius: 4px;
        padding: 0 6px;
        font-size: 0.5 rem;
    }
    .above{
        top: 0;
        left: 24px;
        background: navy;
        border: 0.5px solid blue;
        font-size: 0.5 rem;
    }
    .center{
        top: 50%;
        left: 8px;
        border: 0.5px solid transparent;
        opacity: 0;
    }
    .error {
        color: crimson;
        font-size: 0.7 rem;
    }
    .preference {
        padding: 14px 0;
        overflow: hidden;
        font-size: 0.8rem;
        display: flex;
        flex-direction: column;
        gap: 4px;
        flex: 1;
    }
    .preference > p {
        position: relative;
        text-align: center;
        width: fit-content;
        margin: 0 auto;
        padding: 0 8px;
    }
    /* .preference > p::after,
    .preference > p::before{
        position: absolute;
        top: 50%;
        left: 0;
        transform: translateY(-50%);
        width: 100%;
        height: 1.5px;
        background: white;

    } */

    .preference .auth {
        display: flex;
        align-items: center;
        gap: 8px;
        color: cyan;
        cursor: pointer;
    }




</style>