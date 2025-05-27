<script>
    import { onMount, onDestroy } from 'svelte';
  import Button from './Button.svelte';
  
    let showButton = false;
    const SCROLL_THRESHOLD = 200; // Pixels to scroll down before showing the button
  
    function handleScroll() {
      showButton = window.scrollY > SCROLL_THRESHOLD;
    }
  
    function scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth' // For a smooth scroll animation
      });
    }
  
    onMount(() => {
      window.addEventListener('scroll', handleScroll);
    });
  
    onDestroy(() => {
      window.removeEventListener('scroll', handleScroll);
    });
  </script>
  
  {#if showButton}
    <Button shape="round" size="md" color="tonal" id="go-to-top" onclick={scrollToTop}>
        ⬆
    </Button>
  {/if}
  
  <style>
    :global(#go-to-top) {
      position: fixed;
      z-index: 50;
      bottom: 24px;
      right: 24px;

      --_level: 2;
    }
  </style>