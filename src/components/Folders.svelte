<script>
  export let activeTab = 1;

  function changeTab(tab) {
    activeTab = tab;
  }

</script>

<style>
  .tab {
    cursor: pointer;
    padding: 10px;
    background-color: lightgray;
    border: 1px solid gray;
    border-radius: 5px;
    margin-right: 5px;
    display: inline-block; /* Added CSS */
  }
  
  .active {
    background-color: gray;
    color: white;
  }
</style>

<div role="button" tabindex="0" class="tab" class:active={activeTab === 1} on:click={() => changeTab(1)} on:keydown={() => {}}>Tab 1</div>
<div role="button" tabindex="0" class="tab" class:active={activeTab === 2} on:click={() => changeTab(2)} on:keydown={() => {}}>Tab 2</div>
<div role="button" tabindex="0" class="tab" class:active={activeTab === 3} on:click={() => changeTab(3)} on:keydown={() => {}}>Tab 3</div>
<div role="button" tabindex="0" class="tab" class:active={activeTab === 4} on:click={() => changeTab(4)} on:keydown={() => {}}>Tab 4</div>