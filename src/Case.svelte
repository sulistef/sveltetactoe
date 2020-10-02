<script>
  import { fade } from 'svelte/transition';
  import _ from 'lodash';

  export var lacase;

	const defineClass = (val) => {
		if (val === "X") return "cross"
		else return "circle";
	};
		
</script>

<div class={defineClass(lacase)}>
  {#if !_.isEmpty(lacase)}
    <span transition:fade>{lacase}</span>
  {/if}
</div>

<style>

  .circle {
    font-size: 36px;
    font-weight: 700;
    color: brown;
  }

  .cross {
    font-size: 36px;
    font-weight: 700;
    color: green;
  }

</style>