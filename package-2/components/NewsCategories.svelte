<script>
  import { onMount, tick } from 'svelte';
  
  export let theme = {};
  
  // News Categories with Smooth Tab Navigation
  let activeTab = 0;
  let tabIndicatorStyle = '';
  let tabContainer;
  
  const categories = [
    { 
      id: 'latest', 
      name: 'Latest', 
      count: 24,
      icon: 'clock'
    },
    { 
      id: 'world', 
      name: 'World', 
      count: 18,
      icon: 'globe'
    },
    { 
      id: 'politics', 
      name: 'Politics', 
      count: 12,
      icon: 'building'
    },
    { 
      id: 'technology', 
      name: 'Technology', 
      count: 31,
      icon: 'cpu'
    },
    { 
      id: 'science', 
      name: 'Science', 
      count: 15,
      icon: 'atom'
    },
    { 
      id: 'health', 
      name: 'Health', 
      count: 9,
      icon: 'heart'
    },
    { 
      id: 'sports', 
      name: 'Sports', 
      count: 22,
      icon: 'trophy'
    },
    { 
      id: 'entertainment', 
      name: 'Entertainment', 
      count: 16,
      icon: 'film'
    }
  ];
  
  // Update tab indicator position
  async function updateIndicator() {
    await tick();
    
    if (tabContainer && categories[activeTab]) {
      const activeTabElement = tabContainer.children[activeTab];
      if (activeTabElement) {
        const containerRect = tabContainer.getBoundingClientRect();
        const tabRect = activeTabElement.getBoundingClientRect();
        
        tabIndicatorStyle = `
          left: ${tabRect.left - containerRect.left}px;
          width: ${tabRect.width}px;
        `;
      }
    }
  }
  
  function setActiveTab(index) {
    activeTab = index;
    updateIndicator();
    
    // In real app: Load category-specific content
    console.log(`Active category: ${categories[index].name}`);
  }
  
  // Initialize indicator position
  onMount(() => {
    updateIndicator();
  });
  
  // Update indicator on window resize
  function handleResize() {
    updateIndicator();
  }
  
  onMount(() => {
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  });
  
  function getIcon(iconName) {
    const icons = {
      clock: '<path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/>',
      globe: '<circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>',
      building: '<rect x="3" y="3" width="18" height="18" rx="2"/><rect x="3" y="9" width="18" height="18"/><rect x="7" y="15" width="2" height="2"/><rect x="11" y="15" width="2" height="2"/><rect x="15" y="15" width="2" height="2"/>',
      cpu: '<rect x="4" y="4" width="16" height="16" rx="2"/><rect x="9" y="9" width="6" height="6"/><rect x="9" y="15" width="6" height="1"/><rect x="3" y="12" width="2" height="2"/><rect x="19" y="12" width="2" height="2"/>',
      atom: '<circle cx="12" cy="12" r="1"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/><path d="M12 2a15.3 15.3 0 0 0 4 10 15.3 15.3 0 0 0 4 10 15.3 15.3 0 0 0-4 10 15.3 15.3 0 0 0-4-10 15.3 15.3 0 0 0-4 10 15.3 15.3 0 0 0 4 10z"/>',
      heart: '<path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>',
      trophy: '<path d="M6 9H4.5a2.5 2.5 0 0 1 0-5C7 4 7 9 7 9h6"/><path d="M18 9h1.5a2.5 2.5 0 0 0 0-5C17 4 17 9 17 9h-6"/><path d="M4 22h16"/><path d="M10 14.66V17c0 .55.47.98.97 1.21C11.52 18.75 13 19 15 19"/><path d="M14 14.66V17c0 .55-.47.98-.97 1.21C13.52 18.75 12 19 10 19"/><path d="M18 22H6"/><path d="M8 2v5"/><path d="M16 2v5"/>',
      film: '<rect x="2" y="2" width="20" height="20" rx="2.18" ry="2.18"/><line x1="7" y1="2" x2="7" y2="22"/><line x1="17" y1="2" x2="17" y2="22"/><line x1="2" y1="12" x2="22" y2="12"/><line x1="2" y1="7" x2="7" y2="7"/><line x1="2" y1="17" x2="7" y2="17"/><line x1="17" y1="17" x2="22" y2="17"/><line x1="17" y1="7" x2="22" y2="7"/>'
    };
    return icons[iconName] || '';
  }
</script>

<section class="categories-section">
  <div class="section-header">
    <h2 class="section-title">Browse by Category</h2>
    <p class="section-subtitle">Stay updated with the latest news in your areas of interest</p>
  </div>
  
  <!-- Smooth Tab Navigation -->
  <div class="tabs-container">
    <div class="tabs-wrapper" bind:this={tabContainer}>
      {#each categories as category, index}
        <button
          class="tab-button"
          class:active={index === activeTab}
          on:click={() => setActiveTab(index)}
          aria-label="Switch to {category.name} category"
        >
          <div class="tab-content">
            <div class="tab-icon">
              {@html getIcon(category.icon)}
            </div>
            <span class="tab-name">{category.name}</span>
            <span class="tab-count">{category.count}</span>
          </div>
        </button>
      {/each}
      
      <!-- Smooth Tab Indicator -->
      <div 
        class="tab-indicator"
        style={tabIndicatorStyle}
      />
    </div>
  </div>
  
  <!-- Category Content Preview -->
  <div class="category-preview">
    <div class="preview-header">
      <h3 class="preview-title">
        {categories[activeTab].name} News
        <span class="preview-count">({categories[activeTab].count} articles)</span>
      </h3>
      <button class="view-all-btn">View All</button>
    </div>
    
    <div class="preview-content">
      <!-- Sample articles for the active category -->
      {#each Array(3) as _, articleIndex}
        <article class="preview-article">
          <div class="article-image">
            <div class="image-placeholder">
              <div class="placeholder-icon">
                {@html getIcon(categories[activeTab].icon)}
              </div>
            </div>
          </div>
          <div class="article-content">
            <h4 class="article-title">
              Sample {categories[activeTab].name} Article {articleIndex + 1}
            </h4>
            <p class="article-excerpt">
              This is a preview of the type of content you'd see in the {categories[activeTab].name} category. 
              Each category contains curated articles from trusted sources.
            </p>
            <div class="article-meta">
              <span class="read-time">3 min read</span>
              <span class="separator">•</span>
              <span class="publish-time">2 hours ago</span>
            </div>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>

<style>
  .categories-section {
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
  
  .tabs-container {
    /* Layout: Tab navigation container */
    margin-bottom: 3rem;
  }
  
  .tabs-wrapper {
    /* Layout: Scrollable tabs on mobile */
    position: relative;
    display: flex;
    gap: 0.5rem;
    overflow-x: auto;
    padding: 0.5rem 0;
    scrollbar-width: none;
    -ms-overflow-style: none;
  }
  
  .tabs-wrapper::-webkit-scrollbar {
    display: none;
  }
  
  .tab-button {
    /* Interactive: Tab button styling */
    background: transparent;
    border: none;
    padding: 0.75rem 1.5rem;
    border-radius: 2rem;
    cursor: pointer;
    color: theme.secondary;
    font-weight: 500;
    font-size: 0.9rem;
    white-space: nowrap;
    transition: all 250ms ease-out;
    position: relative;
    
    /* Motion: Subtle hover feedback */
  }
  
  .tab-button:hover {
    /* Feedback: Hover state */
    color: theme.text;
    background: rgba(127, 127, 127, 0.1);
  }
  
  .tab-button.active {
    /* Hierarchy: Active state prominence */
    color: theme.text;
    font-weight: 600;
  }
  
  .tab-content {
    /* Layout: Tab content organization */
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  
  .tab-icon {
    /* Visual: Tab icons */
    width: 18px;
    height: 18px;
    color: currentColor;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .tab-icon :global(svg) {
    width: 100%;
    height: 100%;
  }
  
  .tab-name {
    /* Typography: Tab names */
  }
  
  .tab-count {
    /* Typography: Article count badge */
    background: theme.accent;
    color: white;
    padding: 0.125rem 0.5rem;
    border-radius: 1rem;
    font-size: 0.75rem;
    font-weight: 600;
    min-width: 1.25rem;
    text-align: center;
  }
  
  .tab-button.active .tab-count {
    /* Visual: Active state badge */
    background: theme.accent;
  }
  
  .tab-indicator {
    /* Smooth Tab Indicator: Purposeful navigation flow */
    position: absolute;
    bottom: 0;
    height: 3px;
    background: theme.accent;
    border-radius: 2px;
    transition: all 300ms cubic-bezier(0.25, 1, 0.5, 1);
    z-index: 1;
    
    /* Motion: Smooth horizontal sliding */
  }
  
  .category-preview {
    /* Layout: Category content preview */
  }
  
  .preview-header {
    /* Layout: Preview header */
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
  }
  
  .preview-title {
    /* Typography: Preview title */
    font-size: 1.5rem;
    font-weight: 600;
    color: theme.text;
    margin: 0;
  }
  
  .preview-count {
    /* Typography: Article count */
    font-size: 1rem;
    color: theme.secondary;
    font-weight: 400;
  }
  
  .view-all-btn {
    /* Interactive: View all button */
    background: theme.accent;
    color: white;
    border: none;
    padding: 0.625rem 1.25rem;
    border-radius: 0.5rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 250ms ease-out;
  }
  
  .view-all-btn:hover {
    /* Motion: Purposeful hover feedback */
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(0, 122, 255, 0.3);
  }
  
  .preview-content {
    /* Layout: Preview articles grid */
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }
  
  .preview-article {
    /* Layout: Individual article preview */
    display: flex;
    gap: 1rem;
    padding: 1.5rem;
    background: theme.surface;
    border-radius: 1rem;
    border: 1px solid rgba(127, 127, 127, 0.1);
    transition: all 250ms ease-out;
    
    /* Motion: Subtle hover effect */
  }
  
  .preview-article:hover {
    /* Feedback: Hover state */
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
    border-color: theme.accent;
  }
  
  .article-image {
    /* Layout: Article image container */
    width: 80px;
    height: 80px;
    flex-shrink: 0;
  }
  
  .image-placeholder {
    /* Visual: Placeholder with category icon */
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, 
      rgba(0, 122, 255, 0.1) 0%, 
      rgba(0, 122, 255, 0.05) 100%);
    border-radius: 0.75rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .placeholder-icon {
    /* Visual: Category icon styling */
    width: 32px;
    height: 32px;
    color: theme.accent;
  }
  
  .placeholder-icon :global(svg) {
    width: 100%;
    height: 100%;
  }
  
  .article-content {
    /* Layout: Article content area */
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  
  .article-title {
    /* Typography: Article titles */
    font-size: 1rem;
    font-weight: 600;
    line-height: 1.3;
    color: theme.text;
    margin: 0 0 0.5rem 0;
    
    /* Limit to 2 lines */
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  
  .article-excerpt {
    /* Typography: Article excerpts */
    font-size: 0.875rem;
    line-height: 1.5;
    color: theme.secondary;
    margin: 0 0 1rem 0;
    flex: 1;
    
    /* Limit to 3 lines */
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  
  .article-meta {
    /* Typography: Article metadata */
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.75rem;
    color: theme.secondary;
  }
  
  .separator {
    opacity: 0.5;
  }
  
  /* Responsive Design */
  @media (max-width: 1024px) {
    .preview-content {
      grid-template-columns: 1fr;
    }
  }
  
  @media (max-width: 768px) {
    .categories-section {
      padding: 3rem 1rem;
    }
    
    .section-title {
      font-size: 2rem;
    }
    
    .preview-header {
      flex-direction: column;
      align-items: flex-start;
      gap: 1rem;
    }
    
    .preview-article {
      padding: 1rem;
    }
    
    .article-image {
      width: 60px;
      height: 60px;
    }
    
    .placeholder-icon {
      width: 24px;
      height: 24px;
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .tab-button,
    .preview-article,
    .view-all-btn,
    .tab-indicator {
      transition: none;
    }
    
    .tab-button:hover,
    .preview-article:hover,
    .view-all-btn:hover {
      transform: none;
    }
  }
</style>