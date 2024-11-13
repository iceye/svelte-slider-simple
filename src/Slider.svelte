<input type="number" value={value} name={name} />

<div class="track">
  <div
    class="progress"
    style={progress} />
  <Thumb bind:pos={pos} on:active={({ detail: v }) => active = v}>
    <slot name="left">
      <slot>
        <div class="thumb" />
      </slot>
    </slot>
  </Thumb>
  
</div>

<script>
  import { createEventDispatcher } from "svelte";
  import Thumb from "./Thumb.svelte";

  const dispatch = createEventDispatcher();

  let name = "";
  let range = false;
  let min = 0;
  let max = 100;
  let step = 1;
  let value = min;
  let pos;
  let active = false;
  let order = false;

  export { name, range, min, max, step, value, order };

  $: if (active) setValue(pos);
  $: if (!active) setPos(value);
  $: min, max, clamp();
  $: progress = `
    left: ${ 0}%;
    right: ${100 - pos * 100}%;
  `;

  function setValue(pos) {
    const offset = min % step;
    const width = max - min
    value = min + pos * width;
    value = Math.round((value - offset) / step) * step + offset;
   
    dispatch("input", value);
  }

  function setPos(value) {
    pos = (Math.min(Math.max(value, min), max) - min) / (max - min);
  }

  function clamp() {
    setPos(value);
    setValue(pos);
  }
</script>

<style>
  input {
    display: none;
  }

  .track {
    margin: 16px 8px;
    position: relative;
    height: 4px;
    width: calc(100% - 16px);
    border-radius: 100vh;
    background: var(--track-bg, #ebebeb);
  }

  .progress {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    border-radius: 100vh;
    background: var(--progress-bg, #8abdff);
  }

  .thumb {
    width: 16px;
    height: 16px;
    border-radius: 100vh;
    background: var(--thumb-bg, #5784fd);
  }
</style>
