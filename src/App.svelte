<script lang="ts">
  import Tailwindcss from './Tailwindcss.svelte';
  
  let title = 'new';
  let lists = [
    {name: title, count: 0}
  ];
  
  function plus(index: number) {
    lists[index].count += 1
    lists = lists
    return lists;
  }
  function minus(index: number){
    lists[index].count == 0 ? lists[index].count : lists[index].count -= 1;
    lists = lists
    return lists;
  }
  function reset(index: number) {
     lists[index].count = 0
     lists = lists
     return lists;
  }
  function newCounter() {
     lists.push({name: title, count: 0});
     lists = lists
     return lists;
  }
  function deleteCounter(index: number) {
     lists.splice(index, 1);
     lists = lists
     return lists;
  }
</script>

<Tailwindcss />
<main>
  <div class="content">
    <h1>Multiple Counter</h1>
    <div>
      {#each lists as list, index}
	<div class="counter my-5 w-96 h-11">
          <input class="ml-4 w-32" type="text" bind:value={list.name}>
	  <p class="ml-10 font-bold">{list.count}</p>
	  <button class="plus ml-12 w-9 h-9 text-white bg-red-400" on:click|stopPropagation={() => plus(index)}>+</button>
          <button class="minus w-9 h-9 text-white bg-blue-500" on:click|stopPropagation={() => minus(index)}>-</button>
	  <button class="reset w-9 h-9 text-white bg-yellow-400" on:click|stopPropagation={() => reset(index)}>0</button>
	  <span class="ml-3" on:click|stopPropagation={() => deleteCounter(index)}>x</span>
	</div>
      {/each}
    </div>
    <div class="new_counter w-96 text-center" on:click={newCounter}>
      <p class="m-0 text-white">new counter</p>
    </div>
    <div>title list:
      {#each lists as list}
	&nbsp;{list.name}
      {/each}
    </div>
    <div>sum of count: {
        lists.reduce(function(sum, element){
          return sum + element.count;
        }, 0)
      }
    </div>
  </div>
</main>

<style>
.content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
h1 {
  font-size: 64px;
}
.plus,
.minus,
.reset {
  border: none;
}
input {
  border-color: #f7fafc;
}
.counter {
  display: flex;
  align-items: center;
  box-shadow:  0 10px 15px -3px rgb(0 0 0 / 10%), 0 4px 6px -2px rgb(0 0 0 / 5%);
  background-color: #f7fafc;
}
.new_counter {
  background-color: #68d391;
}
</style>
  
