<script lang="ts">
    import type { ButtonSize, ButtonShape, ButtonStyle } from '../types/Button';
    import type { HTMLButtonAttributes } from 'svelte/elements';
    
    let { size, shape, color, children, ...props }
        : { size: ButtonSize; shape: ButtonShape; color: ButtonStyle; children: any; }
        & HTMLButtonAttributes = $props();

    const classes = [shape, size, color];
</script>

<button
    class={classes.join(' ')}
    {...props}
>
    {@render children?.()}
</button>