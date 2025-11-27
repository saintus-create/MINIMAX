<script>
  import { onMount } from 'svelte';
  import ShimmerText from './ShimmerText.svelte';
  
  export let theme;
  
  // Bento Grid Layout: Structured news organization
  let stories = [];
  let isLoading = true;
  
  // Sample news data - in real app this would come from API
  const sampleStories = [
    {
      id: 1,
      title: "AI Breakthrough: New Language Model Achieves Human-Level Reasoning",
      category: "Technology",
      author: "Dr. Emily Chen",
      readTime: "5 min read",
      image: "https://images.unsplash.com/photo-1677442136019-21780ecad995?w=500&h=300&fit=crop&crop=center",
      featured: true,
      size: "large"
    },
    {
      id: 2,
      title: "Global Markets Surge on Renewable Energy Investment",
      category: "Business", 
      author: "Michael Rodriguez",
      readTime: "3 min read",
      image: "https://images.unsplash.com/photo-1497435334941-8c899ee9e8e9?w=400&h=250&fit=crop&crop=center",
      featured: false,
      size: "medium"
    },
    {
      id: 3,
      title: "Mars Mission: Perseverance Rover Discovers Ancient Microbial Life",
      category: "Science",
      author: "Dr. Sarah Kim",
      readTime: "7 min read", 
      image: "https://images.unsplash.com/photo-1614728894747-a83421e2b9c9?w=400&h=250&fit=crop&crop=center",
      featured: false,
      size: "medium"
    },
    {
      id: 4,
      title: "Tech Giants Announce Joint Initiative for Digital Privacy",
      category: "Technology",
      author: "James Wilson",
      readTime: "4 min read",
      image: "https://images.unsplash.com/photo-1551650975-87deedd944c3?w=400&h=250&fit=crop&crop=center",
      featured: false,
      size: "small"
    },
    {
      id: 5,
      title: "Climate Report: Arctic Ice Levels Reach Record Low",
      category: "Environment",
      author: "Dr. Lisa Thompson",
      readTime: "6 min read",
      image: "https://images.unsplash.com/photo-1578662996442-48f60103fc96?w=400&h=250&fit=crop&crop=center",
      featured: false,
      size: "small"
    },
    {
      id: 6,
      title: "Space Tourism: Virgin Galactic Launches First Commercial Flight",
      category: "Technology",
      author: "Captain Mark Davis",
      readTime: "5 min read",
      image: "https://images.unsplash.com/photo-1446776653964-20c1d3a81b06?w=500&h=300&fit=crop&crop=center",
      featured: true,
      size: "large"
    }
  ];
  
  // Simulate loading with Shimmer effect
  onMount(() => {
    setTimeout(() => {
      stories = sampleStories;
      isLoading = false;
    }, 2000); // 2 second loading simulation
  });
  
  function formatTimeAgo(date) {
    const now = new Date();
    const diff = now.getTime() - date.getTime();
    const hours = Math.floor(diff / (1000 * 60 * 60));
    return `${hours} hours ago`;
  }
</script>

<section class="featured-section">
  <div class="section-header">
    <h2 class="section-title">Featured Stories</h2>
    <p class="section-subtitle">Today's most important news and analysis</p>
  </div>
  
  <!-- Bento Grid Layout with Liquid Glass Cards -->
  <div class="bento-grid">
    {#if isLoading}
      <!-- Shimmer Loading State - Purposeful feedback -->
      {#each Array(6) as _, index}
        <div class="story-card skeleton" style="grid-area: area-{index + 1}">
          <div class="skeleton-image"></div>
          <div class="skeleton-content">
            <div class="skeleton-title"></div>
            <div class="skeleton-meta"></div>
          </div>
        </div>
      {/each}
    {:else}
      {#each stories as story, index}
        <article 
          class="story-card liquid-glass"
          class:large={story.size === 'large'}
          class:medium={story.size === 'medium'}
          class:small={story.size === 'small'}
          class:featured={story.featured}
          style="grid-area: area-{index + 1};"
        >
          <!-- Card Image with Mouse Effect -->
          <div class="card-image-container">
            <img 
              src={story.image}
              alt={story.title}
              class="card-image"
              loading="lazy"
            />
            <div class="image-overlay">
              <button class="read-more-btn">Read Story</button>
            </div>
            <!-- Category Badge -->
            <div class="category-badge">
              {story.category}
            </div>
          </div>
          
          <!-- Card Content -->
          <div class="card-content">
            <h3 class="card-title">{story.title}</h3>
            
            <div class="card-meta">
              <span class="author">{story.author}</span>
              <span class="separator">•</span>
              <span class="read-time">{story.readTime}</span>
            </div>
            
            <!-- Interactive Elements -->
            <div class="card-actions">
              <button class="action-btn bookmark">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M19 21l-7-5-7 5V5a2 2 0 0 1 2-2h10a2 2 0 0 1 2 2z"/>
                </svg>
              </button>
              
              <button class="action-btn share">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="18" cy="5" r="3"/>
                  <circle cx="6" cy="12" r="3"/>
                  <circle cx="18" cy="19" r="3"/>
                  <line x1="8.59" y1="13.51" x2="15.42" y2="17.49"/>
                  <line x1="15.41" y1="6.51" x2="8.59" y2="10.49"/>
                </svg>
              </button>
            </div>
          </div>
        </article>
      {/each}
    {/if}
  </div>
</section>

<style>
  .featured-section {
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
  
  .bento-grid {
    /* Bento Grid: Structured layout system */
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(3, 200px);
    gap: 1.5rem;
    grid-template-areas:
      "area-1 area-1 area-2 area-2"
      "area-1 area-1 area-3 area-4"
      "area-5 area-6 area-3 area-4";
  }
  
  /* Card Layout Variations */
  .story-card.large {
    grid-row: span 2;
    grid-column: span 2;
  }
  
  .story-card.medium {
    grid-row: span 1;
    grid-column: span 2;
  }
  
  .story-card.small {
    grid-row: span 1;
    grid-column: span 1;
  }
  
  /* Liquid Glass Effect */
  .liquid-glass {
    /* Advanced Visual: Glass morphism */
    background: rgba(255, 255, 255, 0.5);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.7);
    border-radius: 1rem;
    overflow: hidden;
    transition: all 300ms ease-out;
    position: relative;
    
    /* Motion: Subtle entrance animation */
    animation: fadeInUp 0.6s ease-out forwards;
  }
  
  @keyframes fadeInUp {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .liquid-glass:hover {
    /* Interactive: Magnetic tilt effect */
    transform: perspective(1000px) rotateX(2deg) rotateY(-2deg) translateY(-8px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
    border-color: rgba(0, 122, 255, 0.3);
  }
  
  /* Skeleton Loading State */
  .skeleton {
    background: rgba(127, 127, 127, 0.1);
    border-radius: 1rem;
    overflow: hidden;
    position: relative;
  }
  
  .skeleton-image {
    /* Shimmer loading effect */
    height: 60%;
    background: linear-gradient(90deg, 
      transparent 0%, 
      rgba(255, 255, 255, 0.4) 50%, 
      transparent 100%);
    animation: shimmer 2s infinite;
  }
  
  .skeleton-content {
    padding: 1rem;
  }
  
  .skeleton-title,
  .skeleton-meta {
    height: 1rem;
    background: rgba(127, 127, 127, 0.2);
    border-radius: 0.25rem;
    margin-bottom: 0.5rem;
    animation: shimmer 2s infinite;
  }
  
  .skeleton-title {
    height: 1.25rem;
  }
  
  @keyframes shimmer {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }
  
  .card-image-container {
    /* Image: Proper aspect ratio and overlay */
    position: relative;
    height: 60%;
    overflow: hidden;
  }
  
  .card-image {
    /* Image: Optimized display */
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 300ms ease-out;
  }
  
  .liquid-glass:hover .card-image {
    /* Motion: Subtle zoom on hover */
    transform: scale(1.05);
  }
  
  .image-overlay {
    /* Interactive: Read story overlay */
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 300ms ease-out;
  }
  
  .liquid-glass:hover .image-overlay {
    opacity: 1;
  }
  
  .read-more-btn {
    /* Interactive: Clear call-to-action */
    background: white;
    color: theme.text;
    border: none;
    padding: 0.75rem 1.5rem;
    border-radius: 0.5rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 250ms ease-out;
  }
  
  .read-more-btn:hover {
    /* Motion: Purposeful hover feedback */
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  }
  
  .category-badge {
    /* Visual: Category indication */
    position: absolute;
    top: 1rem;
    left: 1rem;
    background: theme.accent;
    color: white;
    padding: 0.375rem 0.75rem;
    border-radius: 1rem;
    font-size: 0.75rem;
    font-weight: 500;
    z-index: 2;
  }
  
  .card-content {
    /* Layout: Content organization */
    padding: 1.5rem;
    height: 40%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  
  .card-title {
    /* Typography: Headline styling */
    font-size: 1.125rem;
    font-weight: 600;
    line-height: 1.3;
    margin: 0 0 0.75rem 0;
    color: theme.text;
    
    /* Limit to 2 lines with ellipsis */
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  
  .card-meta {
    /* Typography: Metadata styling */
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.875rem;
    color: theme.secondary;
    margin-bottom: 1rem;
  }
  
  .author {
    font-weight: 500;
  }
  
  .separator {
    opacity: 0.5;
  }
  
  .card-actions {
    /* Layout: Action buttons */
    display: flex;
    gap: 0.5rem;
    margin-top: auto;
  }
  
  .action-btn {
    /* Interactive: Icon buttons */
    background: transparent;
    border: 1px solid rgba(127, 127, 127, 0.3);
    border-radius: 0.5rem;
    padding: 0.5rem;
    cursor: pointer;
    color: theme.secondary;
    transition: all 250ms ease-out;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .action-btn:hover {
    /* Motion: Purposeful hover feedback */
    background: theme.accent;
    color: white;
    border-color: theme.accent;
    transform: scale(1.1);
  }
  
  /* Responsive Design */
  @media (max-width: 1024px) {
    .bento-grid {
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(4, 200px);
      grid-template-areas:
        "area-1 area-1 area-2"
        "area-1 area-1 area-3"
        "area-4 area-5 area-3"
        "area-4 area-6 area-6";
    }
  }
  
  @media (max-width: 768px) {
    .featured-section {
      padding: 3rem 1rem;
    }
    
    .bento-grid {
      grid-template-columns: 1fr;
      grid-template-rows: auto;
      grid-template-areas:
        "area-1"
        "area-2"
        "area-3"
        "area-4"
        "area-5"
        "area-6";
      gap: 1rem;
    }
    
    .story-card {
      grid-column: span 1 !important;
      grid-row: span 1 !important;
      height: 250px;
    }
    
    .section-title {
      font-size: 2rem;
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .liquid-glass,
    .card-image,
    .action-btn,
    .image-overlay {
      transition: none;
    }
    
    .liquid-glass:hover {
      transform: none;
    }
    
    .card-image:hover {
      transform: none;
    }
    
    .action-btn:hover {
      transform: none;
    }
    
    @keyframes fadeInUp,
    @keyframes shimmer {
      animation: none;
    }
  }
</style>