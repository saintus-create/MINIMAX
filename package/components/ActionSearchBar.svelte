<script>
  import { onMount, tick } from 'svelte';
  
  export let theme = {};
  
  // Action Search Bar: Purposeful expansion and interaction flow
  let searchQuery = '';
  let isExpanded = false;
  let isFocused = false;
  let searchInput;
  let searchResults = [];
  let showResults = false;
  
  // Sample search data - in real app would come from API
  const sampleResults = [
    { id: 1, title: 'Climate Change Summit 2024', type: 'article', category: 'Environment' },
    { id: 2, title: 'AI Breakthrough in Language Models', type: 'article', category: 'Technology' },
    { id: 3, title: 'Mars Mission Updates', type: 'article', category: 'Science' },
    { id: 4, title: 'Global Market Trends', type: 'article', category: 'Business' },
    { id: 5, title: 'Tech Giants Privacy Initiative', type: 'article', category: 'Technology' }
  ];
  
  // Search flow management
  function handleSearchIconClick() {
    isExpanded = true;
    tick().then(() => {
      searchInput?.focus();
    });
  }
  
  function handleFocus() {
    isFocused = true;
    showResults = searchQuery.length > 0;
  }
  
  function handleBlur() {
    // Delay hiding results to allow clicking
    setTimeout(() => {
      isFocused = false;
      showResults = false;
    }, 150);
  }
  
  function handleInput() {
    if (searchQuery.length > 0) {
      // Filter results based on query
      searchResults = sampleResults.filter(result => 
        result.title.toLowerCase().includes(searchQuery.toLowerCase())
      );
      showResults = true;
    } else {
      showResults = false;
    }
  }
  
  function handleKeydown(event) {
    if (event.key === 'Escape') {
      closeSearch();
    }
  }
  
  function closeSearch() {
    isExpanded = false;
    showResults = false;
    searchQuery = '';
    isFocused = false;
  }
  
  function selectResult(result) {
    searchQuery = result.title;
    showResults = false;
    // In real app: navigate to article or perform action
  }
  
  // Click outside to close
  onMount(() => {
    function handleClickOutside(event) {
      if (isExpanded && !event.target.closest('.search-container')) {
        closeSearch();
      }
    }
    
    document.addEventListener('click', handleClickOutside);
    return () => document.removeEventListener('click', handleClickOutside);
  });
</script>

<div class="search-container">
  <!-- Search Icon Button - Initial State -->
  {#if !isExpanded}
    <button 
      class="search-icon-button"
      on:click={handleSearchIconClick}
      aria-label="Open search"
    >
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <circle cx="11" cy="11" r="8"/>
        <path d="M21 21l-4.35-4.35"/>
      </svg>
    </button>
  {/if}
  
  <!-- Expanded Search Interface -->
  {#if isExpanded}
    <div class="search-expanded">
      <div class="search-input-container">
        <div class="search-icon">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8"/>
            <path d="M21 21l-4.35-4.35"/>
          </svg>
        </div>
        
        <input
          bind:this={searchInput}
          bind:value={searchQuery}
          on:focus={handleFocus}
          on:blur={handleBlur}
          on:input={handleInput}
          on:keydown={handleKeydown}
          type="text"
          placeholder="Search news, topics, and articles..."
          class="search-input"
        />
        
        <button 
          class="close-button"
          on:click={closeSearch}
          aria-label="Close search"
        >
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <line x1="18" y1="6" x2="6" y2="18"/>
            <line x1="6" y1="6" x2="18" y2="18"/>
          </svg>
        </button>
      </div>
      
      <!-- Search Results Dropdown -->
      {#if showResults}
        <div class="search-results">
          {#if searchResults.length > 0}
            {#each searchResults as result, index}
              <button
                class="search-result-item"
                on:click={() => selectResult(result)}
                style="animation-delay: {index * 50}ms;"
              >
                <div class="result-content">
                  <div class="result-title">{result.title}</div>
                  <div class="result-meta">
                    <span class="result-category">{result.category}</span>
                    <span class="result-type">{result.type}</span>
                  </div>
                </div>
                <div class="result-arrow">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polyline points="9,18 15,12 9,6"/>
                  </svg>
                </div>
              </button>
            {/each}
          {:else}
            <div class="no-results">
              <div class="no-results-icon">
                <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1">
                  <circle cx="11" cy="11" r="8"/>
                  <path d="M21 21l-4.35-4.35"/>
                </svg>
              </div>
              <div class="no-results-text">No results found for "{searchQuery}"</div>
            </div>
          {/if}
        </div>
      {/if}
    </div>
  {/if}
</div>

<style>
  .search-container {
    /* Layout: Search component positioning */
    position: relative;
  }
  
  .search-icon-button {
    /* Interactive: Icon button with clear affordance */
    background: transparent;
    border: none;
    padding: 0.75rem;
    border-radius: 0.5rem;
    cursor: pointer;
    color: theme.secondary;
    transition: all 250ms ease-out;
    display: flex;
    align-items: center;
    justify-content: center;
    
    /* Motion: Purposeful hover feedback */
  }
  
  .search-icon-button:hover {
    color: theme.text;
    background: rgba(127, 127, 127, 0.1);
    transform: scale(1.05);
  }
  
  .search-expanded {
    /* Layout: Expanded search interface */
    display: flex;
    flex-direction: column;
    min-width: 320px;
    animation: expandWidth 300ms ease-out;
  }
  
  @keyframes expandWidth {
    from {
      width: 48px;
      opacity: 0;
    }
    to {
      width: 320px;
      opacity: 1;
    }
  }
  
  .search-input-container {
    /* Layout: Input with icons */
    display: flex;
    align-items: center;
    background: theme.surface;
    border: 2px solid transparent;
    border-radius: 0.75rem;
    padding: 0.75rem 1rem;
    gap: 0.75rem;
    transition: all 250ms ease-out;
    
    /* Focus: Border highlight */
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .search-input-container:focus-within {
    border-color: theme.accent;
    box-shadow: 0 4px 16px rgba(0, 122, 255, 0.15);
  }
  
  .search-icon {
    /* Visual: Search icon styling */
    color: theme.secondary;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .search-input {
    /* Typography: Search input styling */
    flex: 1;
    background: transparent;
    border: none;
    outline: none;
    font-size: 1rem;
    color: theme.text;
    font-family: inherit;
  }
  
  .search-input::placeholder {
    color: theme.secondary;
  }
  
  .close-button {
    /* Interactive: Close button */
    background: transparent;
    border: none;
    padding: 0.25rem;
    border-radius: 0.25rem;
    cursor: pointer;
    color: theme.secondary;
    transition: all 200ms ease-out;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .close-button:hover {
    color: theme.text;
    background: rgba(127, 127, 127, 0.1);
  }
  
  .search-results {
    /* Layout: Results dropdown */
    background: theme.surface;
    border: 1px solid rgba(127, 127, 127, 0.2);
    border-radius: 0.75rem;
    margin-top: 0.5rem;
    max-height: 400px;
    overflow-y: auto;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    
    /* Animation: Smooth appearance */
    animation: slideDown 200ms ease-out;
  }
  
  @keyframes slideDown {
    from {
      opacity: 0;
      transform: translateY(-10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .search-result-item {
    /* Interactive: Result item styling */
    width: 100%;
    background: transparent;
    border: none;
    padding: 1rem;
    cursor: pointer;
    transition: background-color 200ms ease-out;
    display: flex;
    align-items: center;
    justify-content: space-between;
    text-align: left;
    border-bottom: 1px solid rgba(127, 127, 127, 0.1);
    
    /* Motion: Staggered appearance */
    animation: fadeInUp 300ms ease-out forwards;
    opacity: 0;
    transform: translateY(10px);
  }
  
  .search-result-item:last-child {
    border-bottom: none;
  }
  
  .search-result-item:hover {
    background: rgba(127, 127, 127, 0.1);
  }
  
  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .result-content {
    /* Layout: Result content area */
    flex: 1;
  }
  
  .result-title {
    /* Typography: Result title */
    font-size: 0.9rem;
    font-weight: 500;
    color: theme.text;
    margin-bottom: 0.25rem;
    line-height: 1.3;
  }
  
  .result-meta {
    /* Typography: Result metadata */
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.8rem;
    color: theme.secondary;
  }
  
  .result-category {
    background: theme.accent;
    color: white;
    padding: 0.125rem 0.5rem;
    border-radius: 0.75rem;
    font-size: 0.7rem;
    font-weight: 500;
  }
  
  .result-type {
    text-transform: capitalize;
  }
  
  .result-arrow {
    /* Visual: Arrow indicator */
    color: theme.secondary;
    opacity: 0.5;
    transition: opacity 200ms ease-out;
  }
  
  .search-result-item:hover .result-arrow {
    opacity: 1;
    color: theme.accent;
  }
  
  .no-results {
    /* Layout: No results state */
    padding: 2rem;
    text-align: center;
  }
  
  .no-results-icon {
    /* Visual: No results icon */
    color: theme.secondary;
    opacity: 0.5;
    margin-bottom: 1rem;
  }
  
  .no-results-text {
    /* Typography: No results message */
    color: theme.secondary;
    font-size: 0.9rem;
  }
  
  /* Responsive Design */
  @media (max-width: 768px) {
    .search-expanded {
      min-width: 280px;
    }
    
    @keyframes expandWidth {
      from {
        width: 48px;
        opacity: 0;
      }
      to {
        width: 280px;
        opacity: 1;
      }
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .search-icon-button,
    .search-expanded,
    .search-result-item,
    .close-button {
      transition: none;
    }
    
    .search-icon-button:hover,
    .close-button:hover {
      transform: none;
    }
    
    .search-result-item {
      animation: none;
      opacity: 1;
      transform: none;
    }
    
    @keyframes expandWidth,
    @keyframes slideDown,
    @keyframes fadeInUp {
      animation: none;
    }
  }
</style>