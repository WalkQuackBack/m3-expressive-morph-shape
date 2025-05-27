<script lang="ts">
  import Button from './Button.svelte';
  import type { ButtonSize, ButtonShape } from '../types/Button';

  const buttons: {
    text: string;
    size: ButtonSize;
    shape: ButtonShape;
  }[] = [
    {
      text: 'Extra small round',
      size: 'xs',
      shape: 'round'
    },
    {
      text: 'Extra small square',
      size: 'xs',
      shape: 'square'
    },

    {
      text: 'Small round',
      size: 'sm',
      shape: 'round'
    },
    {
      text: 'Small square',
      size: 'sm',
      shape: 'square'
    },
    
    {
      text: 'Medium round',
      size: 'md',
      shape: 'round'
    },
    {
      text: 'Medium square',
      size: 'md',
      shape: 'square'
    },

    {
      text: 'Large round',
      size: 'lg',
      shape: 'round'
    },
    {
      text: 'Large square',
      size: 'lg',
      shape: 'square'
    },

    {
      text: 'Extra Large round',
      size: 'xl',
      shape: 'round'
    },
    {
      text: 'Extra Large square',
      size: 'xl',
      shape: 'square'
    },
  ]
</script>

<div class="wrapper">
  <ul class="buttons">
    <h3>Elevated</h3>
    {#each buttons as button}
      <Button style='width:fit-content' size={button.size} shape={button.shape} color='elevated'>
        {button.text}
      </Button>
    {/each}
  </ul>

  <ul class="buttons">
    <h3>Filled</h3>
    {#each buttons as button}
      <Button style='width:fit-content' size={button.size} shape={button.shape} color='filled'>
        {button.text}
      </Button>
    {/each}
  </ul>

  <ul class="buttons">
    <h3>Tonal</h3>
    {#each buttons as button}
      <Button style='width:fit-content' size={button.size} shape={button.shape} color='tonal'>
        {button.text}
      </Button>
    {/each}
  </ul>

  <ul class="buttons">
    <h3>Outlined</h3>
    {#each buttons as button}
      <Button style='width:fit-content' size={button.size} shape={button.shape} color='outlined'>
        {button.text}
      </Button>
    {/each}
  </ul>

  <ul class="buttons">
    <h3>Text</h3>
    {#each buttons as button}
      <Button style='width:fit-content' size={button.size} shape={button.shape} color='text'>
        {button.text}
      </Button>
    {/each}
  </ul>
</div>

<style>
  .buttons {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 24px;

    list-style: none;
    padding-inline: 0;

    & > h3 {
      margin-block: -0.25em;
    }
  }
  .wrapper {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 24px;
  }
</style>