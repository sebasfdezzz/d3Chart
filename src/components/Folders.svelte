<script lang="ts">
  export let activeTab: Number = 1;

  function changeTab(tab: Number) {
    activeTab = tab;
  }

</script>

<style>
  .tab {
    cursor: pointer;
    padding: 10px;
    background-color: transparent;
    border-radius: 5px;
    color: rgb(172, 172, 172);
    margin-right: 5px;
    display: inline-block; /* Added CSS */
  }
  
  .active {
    background-color: #ff5353!important;
    color: white;
    border-radius: 50px;
  }
</style>

<div role="button" tabindex="0" class="tab" class:active={activeTab === 1} on:click={() => changeTab(1)} on:keydown={() => {}}>All Respondents</div>
<div role="button" tabindex="0" class="tab" class:active={activeTab === 2} on:click={() => changeTab(2)} on:keydown={() => {}}>Professional Developers</div>
<div role="button" tabindex="0" class="tab" class:active={activeTab === 3} on:click={() => changeTab(3)} on:keydown={() => {}}>Learning To Code</div>
<div role="button" tabindex="0" class="tab" class:active={activeTab === 4} on:click={() => changeTab(4)} on:keydown={() => {}}>Other Coders</div>