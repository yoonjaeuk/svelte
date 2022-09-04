<script>
import { onDestroy } from "svelte";
import {setContext} from 'svelte';
import Nested from "../Components/Nested.svelte";
import {count} from '../stores/stores.js';


setContext("name2", "jaeuk")

    
    let name = "Yoon";
    let yes = true;
    let options = [
        {v:1, t:"Seoul"},
        {v:2, t:"Busan"},
        {v:3, t:"Incheon"},
    ]
    let selectedOption = 1;
    let seconds = 0;

    let interval = window.setInterval(() => {
        seconds = seconds + 1;
    }, 1000);

    onDestroy(() => {
        window.clearInterval(interval);
    })


    function updateCount(){
        count.update(n => n + 1);
    }

    const unsubscribe = count.subscribe(value => {
        alert(value);
    });

    onDestroy(unsubscribe);

    //writable store - 쓰기
    //readable store - 읽기
    //derived store - 기존 스토어를 가지고 세로운 스토어를 만듬
</script>

<Nested />

<button type = "button" on:click = {updateCount}>Count</button>
<input type = "text" value ={name} />
<p>Hello {name}</p>

<label><input type = "checkbox" bind:checked={yes} />체크박스 테스트</label>

{#if yes}
  <p>Yes</p>
{:else}
  <p>No</p>
{/if}

<select bind:value = {selectedOption}>
    {#each options as opt}
       <option value = {opt.v}>{opt.t}</option>
    {/each}   

</select>

<p>Selected option is: {selectedOption}</p>
<h1>Hello {seconds}</h1>


