<script>
  export let width = '200px';
  export let height = '20px';
  export let lines = 1;
  export let theme = {};
  
  // ShimmerText component for loading states
  // Implements Signal-to-Noise Ratio: Shows structure without content
</script>

<div class="shimmer-container">
  {#each Array(lines) as _, index}
    <div 
      class="shimmer-line"
      style="width: {lines === 1 ? width : (index === 0 ? '80%' : index === lines - 1 ? '60%' : '90%')}; height: {height};"
    />
  {/each}
</div>

<style>
  .shimmer-container {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
  
  .shimmer-line {
    /* Shimmer loading effect - flows left to right */
    background: linear-gradient(90deg, 
      transparent 0%, 
      rgba(127, 127, 127, 0.2) 50%, 
      transparent 100%);
    border-radius: 0.25rem;
    animation: shimmer 2s infinite;
    position: relative;
    overflow: hidden;
  }
  
  @keyframes shimmer {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .shimmer-line {
      animation: none;
      background: rgba(127, 127, 127, 0.2);
    }
  }
</style>