
<script>
  import { onMount } from 'svelte';
  import { Network } from 'vis-network';
  
  let container;

  onMount(() => {

    // create the array of nodes
    const nodes = [
    { id: 1, label: "NVIDIA"},
    {id:2, label:"OPENAI"},
    {id:3, label:"AMD"},
    {id:4, label:"BROADCOM"},
    {id:5, label:"COREWEAVE"}
]

// create an array of edges for the nodes
const edges = [
    {from: 1, to: 3}
]



const data = {nodes, edges};

const options = {};

const network = new Network(container, data, options);

});
</script>

<div bind:this={container}></div>



<style>
    div{
        width: 100%;
        height: 100%;
        border: 1px solid black;
    }
</style>