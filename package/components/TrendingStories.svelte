<script>
  import { onMount } from 'svelte';
  
  export let theme = {};
  
  // X Card and Mouse Effect Card for Trending Stories
  let trendingStories = [];
  let isLoading = true;
  
  const sampleTrendingStories = [
    {
      id: 1,
      title: "Breaking: Major Earthquake Strikes California Coast",
      category: "World",
      author: "Maria Santos",
      readTime: "4 min read",
      image: "https://images.unsplash.com/photo-1581833971358-2c8b550f87b3?w=300&h=200&fit=crop&crop=center",
      trending: true,
      trendingRank: 1,
      cardStyle: "x-card"
    },
    {
      id: 2,
      title: "Tesla Unveils Revolutionary Battery Technology",
      category: "Technology",
      author: "David Kim",
      readTime: "6 min read",
      image: "https://images.unsplash.com/photo-1617788138017-80ad40651399?w=300&h=200&fit=crop&crop=center",
      trending: true,
      trendingRank: 2,
      cardStyle: "mouse-effect"
    },
    {
      id: 3,
      title: "Stock Market Reaches All-Time High Amid Economic Optimism",
      category: "Business",
      author: "Jennifer Wu",
      readTime: "5 min read",
      image: "https://images.unsplash.com/photo-1611974789855-9c2a0a7236a3?w=300&h=200&fit=crop&crop=center",
      trending: true,
      trendingRank: 3,
      cardStyle: "x-card"
    },
    {
      id: 4,
      title: "Scientists Discover Potential Cure for Alzheimer's",
      category: "Science",
      author: "Dr. Robert Chen",
      readTime: "8 min read",
      image: "https://images.unsplash.com/photo-1559757148-5c350d0d3c56?w=300&h=200&fit=crop&crop=center",
      trending: true,
      trendingRank: 4,
      cardStyle: "mouse-effect"
    },
    {
      id: 5,
      title: "Championship Finals Draw Record Television Audience",
      category: "Sports",
      author: "Michael Thompson",
      readTime: "3 min read",
      image: "https://images.unsplash.com/photo-1461896836934-ffe607ba8211?w=300&h=200&fit=crop&crop=center",
      trending: true,
      trendingRank: 5,
      cardStyle: "x-card"
    },
    {
      id: 6,
      title: "Hollywood A-Listers Gather for Exclusive Film Premiere",
      category: "Entertainment",
      author: "Sarah Johnson",
      readTime: "4 min read",
      image: "https://images.unsplash.com/photo-1489599365723-45d4f6b7f6b1?w=300&h=200&fit=crop&crop=center",
      trending: true,
      trendingRank: 6,
      cardStyle: "mouse-effect"
    }
  ];
  
  // Simulate loading with staggered appearance
  onMount(() => {
    setTimeout(() => {
      trendingStories = sampleTrendingStories;
      isLoading = false;
    }, 1500);
  });
  
  // Mouse effect tracking for interactive cards
  let mouseX = 0;
  let mouseY = 0;
  
  function handleMouseMove(event) {
    const rect = event.currentTarget.getBoundingClientRect();
    mouseX = ((event.clientX - rect.left) / rect.width) * 100;
    mouseY = ((event.clientY - rect.top) / rect.height) * 100;
  }
  
  function handleMouseLeave(event) {
    mouseX = 50; // Reset to center
    mouseY = 50;
  }
  
  function shareStory(story) {
    // Simulate social sharing
    console.log(`Sharing: ${story.title}`);
    
    // In real app: Open share dialog or copy link
    if (navigator.share) {
      navigator.share({
        title: story.title,
        text: `Check out this trending story: ${story.title}`,
        url: window.location.href
      });
    } else {
      // Fallback: Copy to clipboard
      navigator.clipboard.writeText(`${story.title} - ${window.location.href}`);
    }
  }
</script>

<section class="trending-section">
  <div class="section-header">
    <h2 class="section-title">Trending Now</h2>
    <p class="section-subtitle">The most popular stories right now</p>
  </div>
  
  <div class="trending-grid">
    {#if isLoading}
      <!-- Skeleton loading state with staggered appearance -->
      {#each Array(6) as _, index}
        <div 
          class="story-card skeleton"
          style="animation-delay: {index * 100}ms;"
        >
          <div class="skeleton-image"></div>
          <div class="skeleton-content">
            <div class="skeleton-ranking"></div>
            <div class="skeleton-title"></div>
            <div class="skeleton-meta"></div>
          </div>
        </div>
      {/each}
    {:else}
      {#each trendingStories as story, index}
        <article
          class="story-card {story.cardStyle}"
          class:x-card={story.cardStyle === 'x-card'}
          class:mouse-effect={story.cardStyle === 'mouse-effect'}
          style="animation-delay: {index * 100}ms;"
          on:mousemove={story.cardStyle === 'mouse-effect' ? handleMouseMove : null}
          on:mouseleave={story.cardStyle === 'mouse-effect' ? handleMouseLeave : null}
        >
          <!-- Trending Rank Badge -->
          <div class="ranking-badge">
            <span class="rank-number">{story.trendingRank}</span>
          </div>
          
          <!-- Image with X Card overlay -->
          <div class="image-container">
            <img 
              src={story.image}
              alt={story.title}
              class="story-image"
              loading="lazy"
            />
            
            <!-- X Card Share Overlay -->
            {#if story.cardStyle === 'x-card'}
              <div class="share-overlay">
                <button 
                  class="share-button"
                  on:click|stopPropagation={() => shareStory(story)}
                  aria-label="Share story"
                >
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <circle cx="18" cy="5" r="3"/>
                    <circle cx="6" cy="12" r="3"/>
                    <circle cx="18" cy="19" r="3"/>
                    <line x1="8.59" y1="13.51" x2="15.42" y2="17.49"/>
                    <line x1="15.41" y1="6.51" x2="8.59" y2="10.49"/>
                  </svg>
                </button>
              </div>
            {/if}
            
            <!-- Mouse Effect Spotlight -->
            {#if story.cardStyle === 'mouse-effect'}
              <div 
                class="mouse-spotlight"
                style="
                  background: radial-gradient(circle at {mouseX}% {mouseY}%, 
                    rgba(255, 255, 255, 0.1) 0%, 
                    transparent 50%);
                "
              />
            {/if}
          </div>
          
          <!-- Content Area -->
          <div class="content">
            <div class="content-header">
              <span class="category">{story.category}</span>
              <span class="read-time">{story.readTime}</span>
            </div>
            
            <h3 class="title">{story.title}</h3>
            
            <div class="content-footer">
              <span class="author">By {story.author}</span>
              <button 
                class="read-button"
                on:click={() => console.log('Read story:', story.id)}
              >
                Read
              </button>
            </div>
          </div>
        </article>
      {/each}
    {/if}
  </div>
</section>

<style>
  .trending-section {
    /* Foundation: Layout with proper spacing */
    padding: 4rem 2rem;
    max-width: 1400px;
    margin: 0 auto;
  }
  
  .section-header {
    /* Typography: Clear section hierarchy */
    text-align: center;
    margin-bottom: 3rem;
  }
  
  .section-title {
    font-size: 2.5rem;
    font-weight: 700;
    margin: 0 0 0.5rem 0;
    color: theme.text;
    letter-spacing: -0.02em;
  }
  
  .section-subtitle {
    font-size: 1.125rem;
    color: theme.secondary;
    margin: 0;
  }
  
  .trending-grid {
    /* Layout: Trending stories grid */
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 1.5rem;
  }
  
  .story-card {
    /* Foundation: Card base styling */
    background: theme.surface;
    border-radius: 1rem;
    overflow: hidden;
    transition: all 300ms ease-out;
    position: relative;
    border: 1px solid rgba(127, 127, 127, 0.1);
    
    /* Motion: Staggered entrance animation */
    animation: fadeInUp 0.6s ease-out forwards;
    opacity: 0;
    transform: translateY(20px);
  }
  
  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  /* X Card Style */
  .story-card.x-card:hover {
    /* Interactive: X Card hover effect */
    transform: translateY(-8px);
    box-shadow: 0 16px 40px rgba(0, 0, 0, 0.15);
    border-color: theme.accent;
  }
  
  /* Mouse Effect Card Style */
  .story-card.mouse-effect {
    /* Interactive: Mouse effect base */
    cursor: none; /* Hide cursor for effect */
  }
  
  .story-card.mouse-effect:hover {
    /* Interactive: Mouse effect hover */
    transform: translateY(-4px) scale(1.02);
    box-shadow: 0 12px 32px rgba(0, 0, 0, 0.12);
  }
  
  .ranking-badge {
    /* Visual: Trending rank positioning */
    position: absolute;
    top: 1rem;
    left: 1rem;
    z-index: 2;
    background: theme.accent;
    color: white;
    width: 32px;
    height: 32px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 0.875rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  }
  
  .image-container {
    /* Layout: Image container with effects */
    position: relative;
    height: 200px;
    overflow: hidden;
  }
  
  .story-image {
    /* Image: Optimized display */
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 300ms ease-out;
  }
  
  .story-card:hover .story-image {
    /* Motion: Subtle zoom on hover */
    transform: scale(1.05);
  }
  
  /* X Card Share Overlay */
  .share-overlay {
    /* Interactive: Share button overlay */
    position: absolute;
    top: 1rem;
    right: 1rem;
    opacity: 0;
    transition: opacity 300ms ease-out;
    z-index: 2;
  }
  
  .story-card.x-card:hover .share-overlay {
    opacity: 1;
  }
  
  .share-button {
    /* Interactive: Share button styling */
    background: rgba(255, 255, 255, 0.9);
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    color: theme.text;
    backdrop-filter: blur(10px);
    transition: all 250ms ease-out;
  }
  
  .share-button:hover {
    /* Motion: Purposeful hover feedback */
    background: white;
    transform: scale(1.1);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  }
  
  /* Mouse Effect Spotlight */
  .mouse-spotlight {
    /* Advanced Visual: Spotlight effect */
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    transition: background 100ms ease-out;
  }
  
  .content {
    /* Layout: Content area */
    padding: 1.5rem;
  }
  
  .content-header {
    /* Layout: Content metadata */
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.75rem;
  }
  
  .category {
    /* Visual: Category badge */
    background: theme.accent;
    color: white;
    padding: 0.25rem 0.75rem;
    border-radius: 1rem;
    font-size: 0.75rem;
    font-weight: 500;
  }
  
  .read-time {
    /* Typography: Reading time */
    font-size: 0.75rem;
    color: theme.secondary;
    font-weight: 500;
  }
  
  .title {
    /* Typography: Article titles */
    font-size: 1.125rem;
    font-weight: 600;
    line-height: 1.3;
    color: theme.text;
    margin: 0 0 1rem 0;
    
    /* Limit to 3 lines */
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  
  .content-footer {
    /* Layout: Footer with author and action */
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .author {
    /* Typography: Author information */
    font-size: 0.875rem;
    color: theme.secondary;
    font-weight: 500;
  }
  
  .read-button {
    /* Interactive: Read button */
    background: theme.accent;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;
    font-weight: 500;
    font-size: 0.875rem;
    cursor: pointer;
    transition: all 250ms ease-out;
  }
  
  .read-button:hover {
    /* Motion: Purposeful hover feedback */
    background: darken(theme.accent, 10%);
    transform: translateY(-1px);
  }
  
  /* Skeleton Loading State */
  .skeleton {
    background: rgba(127, 127, 127, 0.1);
    border-radius: 1rem;
    overflow: hidden;
    position: relative;
    animation: fadeInUp 0.6s ease-out forwards;
  }
  
  .skeleton-image {
    height: 200px;
    background: rgba(127, 127, 127, 0.2);
    position: relative;
  }
  
  .skeleton-image::after {
    /* Shimmer effect for image */
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(90deg, 
      transparent 0%, 
      rgba(255, 255, 255, 0.4) 50%, 
      transparent 100%);
    animation: shimmer 2s infinite;
  }
  
  .skeleton-content {
    padding: 1.5rem;
  }
  
  .skeleton-ranking {
    width: 32px;
    height: 32px;
    background: rgba(127, 127, 127, 0.2);
    border-radius: 50%;
    margin-bottom: 1rem;
  }
  
  .skeleton-title {
    height: 1.25rem;
    background: rgba(127, 127, 127, 0.2);
    border-radius: 0.25rem;
    margin-bottom: 0.75rem;
  }
  
  .skeleton-meta {
    height: 1rem;
    background: rgba(127, 127, 127, 0.2);
    border-radius: 0.25rem;
    width: 60%;
  }
  
  @keyframes shimmer {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }
  
  /* Utility function for darken (CSS custom property) */
  @property --accent-dark {
    syntax: '<color>';
    inherits: false;
    initial-value: theme.accent;
  }
  
  /* Responsive Design */
  @media (max-width: 768px) {
    .trending-section {
      padding: 3rem 1rem;
    }
    
    .trending-grid {
      grid-template-columns: 1fr;
      gap: 1rem;
    }
    
    .section-title {
      font-size: 2rem;
    }
    
    .story-card.mouse-effect {
      cursor: default; /* Restore cursor on mobile */
    }
    
    .image-container {
      height: 160px;
    }
    
    .content {
      padding: 1rem;
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .story-card,
    .share-button,
    .read-button,
    .story-image,
    .mouse-spotlight {
      transition: none;
    }
    
    .story-card:hover,
    .share-button:hover,
    .read-button:hover {
      transform: none;
    }
    
    .story-card:hover .story-image {
      transform: none;
    }
    
    @keyframes fadeInUp,
    @keyframes shimmer {
      animation: none;
    }
    
    .story-card,
    .skeleton {
      opacity: 1;
      transform: none;
    }
  }
</style>