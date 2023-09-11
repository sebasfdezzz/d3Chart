<script lang="ts">
    import Folders from "../components/Folders.svelte";
    import Chart from "../components/Chart.svelte"
    import {data1, data2, data3, data4} from '../data/datas';
    let tab = 1
    $: currentTab = tab
    function getDataForTab(tab: Number) {
        switch (tab) {
            case 1:
                return data1;
            case 2:
                return data2;
            case 3:
                return data3;
            case 4:
                return data4;
            default:
                return [];
        }
    }
</script>
  
<main style="padding-left: 100px;">
    <div><Folders bind:activeTab={tab} /></div>
    <Chart data={getDataForTab(currentTab)} />
</main>

