
<script>
  import { onMount } from 'svelte';
  import { Network } from 'vis-network';
  
  let container;

  onMount(() => {

    // create the array of nodes
    const nodes = [
    { id: 1, label: "NVIDIA MKT CAP: $4.5T, $72.88B Net"},
    {id:2, label:"OPENAI Valuation: $500B"},
    {id:3, label:"AMD MKT CAP: $361B, $3.3B Net"},
    {id:4, label:"ORACLE MKT CAP: $629.6B, $12.4B Net"},
    {id:5, label:"COREWEAVE MKT CAP: $34B, $-0.74B Net"}
]

// create an array of edges for the nodes
const edges = [
    {from: 2, to: 5, label: 'OpenAI invests into Coreweave, $11.9B', url:'https://www.coreweave.com/news/coreweave-announces-agreement-with-openai-to-deliver-ai-infrastructure'},
    {from: 2, to: 5, label: 'OpenAI EXPANDS investment into Coreweave, $6.5B', url:'https://www.reuters.com/business/coreweave-expands-openai-pact-with-new-65-billion-contract-2025-09-25/'},
    {from: 5, to: 2, label: 'CoreWeave issues shares totalling $350M to OpenAI', url:'https://finance.yahoo.com/news/exclusive-coreweave-strikes-12-billion-182359450.html'},
    {from: 2, to: 3, label: 'OpenAI to purchase and deploy AMD tech', url:'https://ir.amd.com/news-events/press-releases/detail/1260/amd-and-openai-announce-strategic-partnership-to-deploy-6-gigawatts-of-amd-gpus'},
    {from: 3, to: 2, label: 'AMD to allow OpenAI to purchase ~10% of AMD stock', url:'https://finance.yahoo.com/news/amd-stock-rockets-higher-on-multibillion-dollar-openai-deal-125503782.html'},
    {from: 2, to: 4, label: 'OpenAI strikes deal worth $300B with Oracle', url:'https://intuitionlabs.ai/articles/oracle-openai-300b-deal-analysis'},
    {from: 2, to: 1, label: 'OpenAI to build and deploy at least 10 gigawatts of AI datacenters with NVIDIA systems', url:'https://intuitionlabs.ai/articles/oracle-openai-300b-deal-analysis'},
    {from: 1, to: 2, label: 'NVIDIA to invest up to $100B in OpenAI per gigawatt deployed', url:'https://intuitionlabs.ai/articles/oracle-openai-300b-deal-analysis'},
    {from: 1, to: 5, label: 'NVIDIA owns $900M of CoreWeave stock', url:'https://www.cnbc.com/2025/05/15/nvidia-owned-900-million-worth-of-coreweave-shares-q1-filing-shows.html'},
    {from: 5, to: 1, label: 'CoreWeave signs $6.3B order with Nvidia', url:'https://www.reuters.com/business/coreweave-nvidia-sign-63-billion-cloud-computing-capacity-order-2025-09-15/'},
    {from: 4, to: 3, label: 'Oracle to deploy 50,000 AMD AI chips', url:'https://www.cnbc.com/2025/10/14/oracle-cloud-to-deploy-50000-amd-ai-chips-as-alternative-to-nvidia.html'}

]



const data = {nodes, edges};

const options = {
      nodes: {
        shape: 'box',  // or 'circle', 'ellipse', 'database', etc.
        margin: 10,    // padding inside the node
        color: 'gray',
        font: {
          size: 20,
          face: 'arial'
        }
      },
      edges: {
        color:{
            color: 'gray',
            highlight: 'red',
            margin: 10
        },

        arrows: {
            to: {
                enabled: true,
                type: 'arrow',
                
            }
        },
        
        font: {
          size: 12,
          align: 'top'  
          
        },
        smooth: {
            enabled: true,
            type: 'dynamic',
            roundness: 1.0  // curves the edge so label has more space
          
        }
      },
      physics: {
        enabled: true,  
        barnesHut: {
          gravitationalConstant: -1000,
          
           
          
          avoidOverlap: 1
        }
      }
    };

const network = new Network(container, data, options);
network.once('stabilizationIterationsDone', function(){
        network.setOptions({physics:false});
    });

    network.on('click', function(params) {
      if (params.edges.length > 0) {
        const edgeId = params.edges[0];
        const edge = edges.find(e => e.id === edgeId);
        console.log('Edge clicked:', edge);

        if (edge && edge.url){
            window.open(edge.url, '_blank');
        }

        }
    });
    network.once('stabilizationIterationsDone', function(){
        network.setOptions({physics:false});
    });

});
</script>

<div bind:this={container}></div>



<style>
    div{
  height: 95vh;
  width: 95vw;
  box-sizing: border-box;
    }
</style>