<script>
  import { onMount } from 'svelte';
  
  export let theme;
  
  // Typography: Breaking news with Typing Text effect
  const headline = "Breaking: Major Climate Summit Reaches Historic Agreement";
  const subheadline = "World leaders unite on unprecedented climate action commitments";
  
  // Animation State Management
  let isTyping = true;
  let displayText = '';
  let currentIndex = 0;
  
  // Typing effect timing - Purposeful pacing
  const typingSpeed = 50; // milliseconds per character
  const pauseDuration = 2000; // pause after completion
  
  function startTypingEffect() {
    const typeCharacter = () => {
      if (currentIndex < headline.length) {
        displayText = headline.slice(0, currentIndex + 1);
        currentIndex++;
        setTimeout(typeCharacter, typingSpeed);
      } else {
        // Add blinking cursor effect
        setTimeout(() => {
          isTyping = false;
        }, pauseDuration);
      }
    };
    
    typeCharacter();
  }
  
  onMount(() => {
    startTypingEffect();
  });
  
  // Beams Background Animation - Subtle, purpose-driven
  let beamPositions = [
    { x: 10, y: 20, opacity: 0.3 },
    { x: 30, y: 60, opacity: 0.2 },
    { x: 70, y: 10, opacity: 0.4 },
    { x: 90, y: 70, opacity: 0.1 }
  ];
  
  let animationFrame;
  
  function animateBeams() {
    beamPositions = beamPositions.map(beam => ({
      ...beam,
      y: (beam.y + 0.5) % 100, // Slow, purposeful movement
      opacity: 0.1 + Math.sin(Date.now() * 0.001 + beam.x * 0.1) * 0.3 // Gentle pulsation
    }));
    
    animationFrame = requestAnimationFrame(animateBeams);
  }
  
  onMount(() => {
    animateBeams();
    return () => cancelAnimationFrame(animationFrame);
  });
</script>

<section class="hero">
  <!-- Beams Background - Purposeful depth creation -->
  <div class="background-effects">
    {#each beamPositions as beam, index}
      <div 
        class="beam"
        style="
          left: {beam.x}%;
          top: {beam.y}%;
          opacity: {beam.opacity};
          animation-delay: {index * 0.5}s;
        "
      />
    {/each}
  </div>
  
  <div class="hero-content">
    <div class="hero-text">
      <!-- Typography Hierarchy: Primary headline with typing effect -->
      <h1 class="hero-headline">
        <span class="typing-container">
          {displayText}
          {#if isTyping}
            <span class="cursor">|</span>
          {/if}
        </span>
      </h1>
      
      <!-- Subheadline: Supporting information -->
      <p class="hero-subheadline">
        {subheadline}
      </p>
      
      <!-- Call-to-action with Purposeful Animation -->
      <div class="hero-actions">
        <button class="cta-button primary">
          Read Full Story
        </button>
        <button class="cta-button secondary">
          Watch Video
        </button>
      </div>
      
      <!-- News metadata with Visual Hierarchy -->
      <div class="news-meta">
        <span class="category">Climate</span>
        <span class="separator">•</span>
        <span class="time">2 hours ago</span>
        <span class="separator">•</span>
        <span class="author">By Sarah Johnson</span>
      </div>
    </div>
    
    <!-- Featured Image with Apple Activity Card style -->
    <div class="hero-visual">
      <div class="featured-image-card">
        <img 
          src="https://images.unsplash.com/photo-1569163139394-de4e4f43e4e5?w=600&h=400&fit=crop&crop=center"
          alt="Climate summit delegates in discussion"
          class="featured-image"
        />
        <div class="image-overlay">
          <div class="play-button">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M8 5v14l11-7z"/>
            </svg>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .hero {
    /* Foundation: Layout with maximum impact */
    position: relative;
    min-height: 550px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 6rem 2rem 4rem;
    overflow: hidden;
    
    /* Background: Clean, professional */
    background: linear-gradient(135deg, 
      rgba(127, 127, 127, 0.05) 0%, 
      rgba(127, 127, 127, 0.02) 100%);
  }
  
  .background-effects {
    /* Advanced Visual: Subtle depth and atmosphere */
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    z-index: 1;
  }
  
  .beam {
    /* Beams Background Effect - Purposeful animation */
    position: absolute;
    width: 2px;
    height: 200%;
    background: linear-gradient(
      to bottom,
      transparent,
      theme.accent,
      transparent
    );
    transform: translateX(-50%) rotate(45deg);
    animation: beamFloat 8s ease-in-out infinite;
  }
  
  @keyframes beamFloat {
    0%, 100% {
      transform: translateX(-50%) rotate(45deg) translateY(-20px);
      opacity: 0.1;
    }
    50% {
      transform: translateX(-50%) rotate(45deg) translateY(20px);
      opacity: 0.4;
    }
  }
  
  .hero-content {
    /* Layout: Balanced two-column design */
    max-width: 1400px;
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 400px;
    gap: 4rem;
    align-items: center;
    position: relative;
    z-index: 2;
  }
  
  .hero-text {
    /* Typography: Readable and impactful */
  }
  
  .hero-headline {
    /* Typography Hierarchy: Maximum impact */
    font-size: 3.5rem;
    font-weight: 700;
    line-height: 1.1;
    margin: 0 0 1.5rem 0;
    color: theme.text;
    letter-spacing: -0.02em;
    
    /* Animation: Smooth text appearance */
    animation: slideInUp 0.8s ease-out;
  }
  
  .typing-container {
    display: inline-block;
  }
  
  .cursor {
    /* Typing Text: Blinking cursor effect */
    color: theme.accent;
    animation: blink 1s infinite;
  }
  
  @keyframes blink {
    0%, 50% { opacity: 1; }
    51%, 100% { opacity: 0; }
  }
  
  .hero-subheadline {
    /* Typography: Supporting information */
    font-size: 1.25rem;
    line-height: 1.6;
    color: theme.secondary;
    margin: 0 0 2.5rem 0;
    max-width: 600px;
    
    /* Animation: Staggered appearance */
    animation: slideInUp 0.8s ease-out 0.2s both;
  }
  
  .hero-actions {
    /* Layout: Action-oriented design */
    display: flex;
    gap: 1rem;
    margin-bottom: 2rem;
    
    /* Animation: Staggered button appearance */
    animation: slideInUp 0.8s ease-out 0.4s both;
  }
  
  .cta-button {
    /* Interactive Design: Clear affordance */
    padding: 0.875rem 1.75rem;
    border: none;
    border-radius: 0.75rem;
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    transition: all 250ms ease-out;
    position: relative;
    overflow: hidden;
  }
  
  .cta-button.primary {
    /* Hierarchy: Primary action prominence */
    background: theme.accent;
    color: white;
    box-shadow: 0 4px 12px rgba(0, 122, 255, 0.3);
  }
  
  .cta-button.primary:hover {
    /* Motion: Purposeful hover feedback */
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0, 122, 255, 0.4);
  }
  
  .cta-button.secondary {
    /* Visual: Secondary action styling */
    background: transparent;
    color: theme.text;
    border: 2px solid theme.secondary;
  }
  
  .cta-button.secondary:hover {
    /* Motion: Subtle hover enhancement */
    background: theme.secondary;
    color: theme.bg;
    transform: translateY(-1px);
  }
  
  .news-meta {
    /* Typography: Metadata with visual separation */
    display: flex;
    align-items: center;
    gap: 0.75rem;
    font-size: 0.875rem;
    color: theme.secondary;
    
    /* Animation: Final staggered element */
    animation: slideInUp 0.8s ease-out 0.6s both;
  }
  
  .category {
    /* Visual: Category highlight */
    background: theme.accent;
    color: white;
    padding: 0.25rem 0.75rem;
    border-radius: 1rem;
    font-weight: 500;
  }
  
  .separator {
    /* Visual: Subtle separator */
    opacity: 0.5;
  }
  
  .hero-visual {
    /* Layout: Balanced visual content */
  }
  
  .featured-image-card {
    /* Apple Activity Card: Premium card design */
    background: theme.surface;
    border-radius: 1rem;
    overflow: hidden;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
    transition: all 300ms ease-out;
    position: relative;
    
    /* Animation: Entrance effect */
    animation: fadeInScale 0.8s ease-out 0.3s both;
  }
  
  .featured-image-card:hover {
    /* Motion: Interactive hover feedback */
    transform: translateY(-4px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
  }
  
  .featured-image {
    /* Image: Optimized display */
    width: 100%;
    height: 300px;
    object-fit: cover;
    display: block;
  }
  
  .image-overlay {
    /* Interactive: Video play affordance */
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    opacity: 0;
    transition: opacity 300ms ease-out;
  }
  
  .featured-image-card:hover .image-overlay {
    opacity: 1;
  }
  
  .play-button {
    /* Visual: Play button styling */
    width: 60px;
    height: 60px;
    background: rgba(255, 255, 255, 0.9);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: theme.accent;
    backdrop-filter: blur(10px);
    transition: all 250ms ease-out;
  }
  
  .play-button:hover {
    /* Motion: Interactive feedback */
    transform: scale(1.1);
    background: white;
  }
  
  /* Keyframe Animations */
  @keyframes slideInUp {
    from {
      opacity: 0;
      transform: translateY(30px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  @keyframes fadeInScale {
    from {
      opacity: 0;
      transform: scale(0.95);
    }
    to {
      opacity: 1;
      transform: scale(1);
    }
  }
  
  /* Responsive Design */
  @media (max-width: 1024px) {
    .hero-content {
      grid-template-columns: 1fr;
      gap: 3rem;
      text-align: center;
    }
    
    .hero-headline {
      font-size: 2.75rem;
    }
  }
  
  @media (max-width: 768px) {
    .hero {
      padding: 4rem 1rem 3rem;
      min-height: auto;
    }
    
    .hero-headline {
      font-size: 2.25rem;
    }
    
    .hero-subheadline {
      font-size: 1.125rem;
    }
    
    .hero-actions {
      flex-direction: column;
      align-items: center;
    }
    
    .cta-button {
      width: 100%;
      max-width: 280px;
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .beam,
    .cursor,
    .hero-headline,
    .hero-subheadline,
    .hero-actions,
    .news-meta,
    .featured-image-card {
      animation: none;
    }
    
    .cta-button:hover,
    .featured-image-card:hover {
      transform: none;
    }
  }
</style>