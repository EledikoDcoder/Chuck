
<script>
    import axios from "axios";
	import { onMount } from "svelte";

    const getJokes = async ()=>{
        const response = await axios.get("https://api.chucknorris.io/jokes/random")
        return response
    }
    $:jokes = []

    onMount(async()=>{ 
        const joke = await getJokes()
        jokes=[joke.data]

        // console.log(jokes);
    })
   

    let refresh = setInterval(async() =>{
        const response = await getJokes()
        jokes = [...jokes,response.data]

        console.log(response)
    },4000)


    function refreshpage() {
        location.reload();
 
    }
    </script>



<div class="flex flex-col w-[100vw] h-[100vh]  bg-gradient-to-r from-cyan-500 to-teal-500 justify-center items-center">
    <div class="flex flex-col w-[20rem] h-[23rem] shadow-lg bg-[#fff] rounded-md p-4">
        <h1 class=" text-center font-bold text-3xl pb-[0.5rem] text-[1.5rem] text-cyan-900">CHUCK NORRIS</h1>

        <div class="flex flex-col gap-[2rem]  overflow-auto">
            {#each jokes as joke}
            <ol class="flex text-1xl w-full pb-4 border-b border-cyan-900 text-cyan-900">
                <li class="list-decimal">{joke.value}</li>
            </ol>
            {/each}
        </div>
    </div>
    <button on:click={refreshpage} class="bg-[#fff] mt-9 py-1.5 px-7  text-cyan-900 text-xl font-bold rounded-md">Restart</button>
</div>
 