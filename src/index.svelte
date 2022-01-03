<svelte:options tag="svelte-progresscircle" />

<script>
  export let value = 0;
  export let max = 100;

  $: progressPath = () => {
    if (value <= 0) {
      return "";
    } else if (value >= max) {
      return "M50,5A45 45 0 1 1 49.9999 5";
    } else {
      const angle = Math.PI * 2 * (value / max);
      const x = 50 + Math.cos(angle - Math.PI / 2) * 45;
      const y = 50 + Math.sin(angle - Math.PI / 2) * 45;

      let path = "M50,5";

      if (angle > Math.PI) {
        path += "A45 45 0 0 1 50 95";
      }

      path += `A45 45 0 0 1 ${x} ${y}`;

      return path;
    }
  };
</script>

<style>
  .svelte-progresscircle svg {
    fill: var(--progress-fill, #def);
    height: 100%;
    position: absolute;
    stroke-linecap: var(--progress-linecap, round);
    width: 100%;
  }
  .svelte-progresscircle svg path:first-child {
    stroke: var(--progress-trackcolor, #bdf);
    stroke-width: var(--progress-trackwidth, 9px);
  }
  .svelte-progresscircle svg path:last-child {
    stroke: var(--progress-color, #28e);
    stroke-width: var(--progress-width, 9px);
  }
  div.svelte-progresscircle {
    height: 28px;
    position: relative;
    width: 28px;
  }
  div.svelte-progresscircle span {
    font-size: 14px;
    font-weight: 300;
    left: 50%;
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
  }
</style>
<div class="svelte-progresscircle">
  <svg viewBox="0 0 100 100">
    <path d="M50,5A45 45 0 1 1 49.9999 5" />
    <path d="{progressPath()}" />
  </svg>
  <div class="svelte-progresscircle">    
  </div>
</div>
