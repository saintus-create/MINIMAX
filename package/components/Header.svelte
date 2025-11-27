<script>
  import ActionSearchBar from './ActionSearchBar.svelte';
  import ProfileDropdown from './ProfileDropdown.svelte';
  
  export let currentTheme;
  export let toggleTheme;
  export let theme;
  
  // Foundation: Layout, Proximity - Group related navigation items
  const navigationItems = [
    { name: 'Latest', href: '#', active: true },
    { name: 'World', href: '#' },
    { name: 'Politics', href: '#' },
    { name: 'Technology', href: '#' },
    { name: 'Sports', href: '#' },
    { name: 'Entertainment', href: '#' },
    { name: 'Business', href: '#' }
  ];
  
  let showProfile = false;
  
  function toggleProfile() {
    showProfile = !showProfile;
  }
</script>

<header class="header">
  <div class="header-content">
    <!-- Logo with Typography Hierarchy -->
    <div class="logo">
      <h1 class="logo-text">NewsHub</h1>
    </div>
    
    <!-- Navigation with Proximity Principle -->
    <nav class="nav" aria-label="Main navigation">
      <ul class="nav-list">
        {#each navigationItems as item}
          <li class="nav-item">
            <a 
              href={item.href}
              class="nav-link"
              class:active={item.active}
            >
              {item.name}
            </a>
          </li>
        {/each}
      </ul>
    </nav>
    
    <!-- Search and Profile with Interactive Design -->
    <div class="header-actions">
      <ActionSearchBar {theme} />
      
      <button 
        class="theme-toggle"
        on:click={toggleTheme}
        aria-label="Toggle theme"
      >
        <div class="theme-icon">
          {#if currentTheme === 'light'}
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="5"/>
              <path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/>
            </svg>
          {:else if currentTheme === 'dark'}
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>
            </svg>
          {:else}
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <rect x="3" y="3" width="7" height="7"/>
              <rect x="14" y="3" width="7" height="7"/>
              <rect x="14" y="14" width="7" height="7"/>
              <rect x="3" y="14" width="7" height="7"/>
            </svg>
          {/if}
        </div>
      </button>
      
      <div class="profile-container">
        <button 
          class="profile-button"
          on:click={toggleProfile}
          aria-label="Profile menu"
        >
          <div class="avatar">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/>
              <circle cx="12" cy="7" r="4"/>
            </svg>
          </div>
        </button>
        
        {#if showProfile}
          <ProfileDropdown onClose={() => showProfile = false} {theme} />
        {/if}
      </div>
    </div>
  </div>
</header>

<style>
  .header {
    /* Foundation: Layout, White Space, Alignment */
    position: sticky;
    top: 0;
    z-index: 100;
    background: theme.surface;
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border-subtle, #E5E5E7);
    transition: all 300ms ease-out;
    
    /* Accessibility: Proper contrast ratios */
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  }
  
  .header-content {
    /* Layout: Grid system with proper proportions */
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 2rem;
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 2rem;
    height: 72px;
  }
  
  .logo {
    /* Typography Hierarchy: Prominent brand identity */
  }
  
  .logo-text {
    /* Foundation: Balance, Visual Weight */
    font-size: 1.5rem;
    font-weight: 700;
    margin: 0;
    color: theme.text;
    letter-spacing: -0.025em;
    transition: color 300ms ease-out;
  }
  
  .nav {
    /* Proximity: Group navigation items together */
  }
  
  .nav-list {
    /* Layout: Horizontal list with consistent spacing */
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
    gap: 2rem;
    align-items: center;
  }
  
  .nav-link {
    /* Interactive Design: Affordance, Feedback */
    color: theme.secondary;
    text-decoration: none;
    font-weight: 500;
    padding: 0.5rem 0;
    position: relative;
    transition: all 250ms ease-out;
    
    /* Focus: Accessibility compliance */
    outline: none;
  }
  
  .nav-link:hover,
  .nav-link:focus {
    color: theme.text;
    /* Motion: Subtle scale for hover feedback */
    transform: translateY(-1px);
  }
  
  .nav-link.active {
    /* Hierarchy: Active state prominence */
    color: theme.text;
    font-weight: 600;
  }
  
  .nav-link.active::after {
    /* Visual indicator for current page */
    content: '';
    position: absolute;
    bottom: -1px;
    left: 0;
    right: 0;
    height: 2px;
    background: theme.accent;
    border-radius: 1px;
  }
  
  .header-actions {
    /* Layout: Right-aligned actions with proper spacing */
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  
  .theme-toggle {
    /* Interactive Element: Theme switching */
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
  }
  
  .theme-toggle:hover {
    color: theme.text;
    background: rgba(127, 127, 127, 0.1);
    transform: scale(1.05);
  }
  
  .theme-icon {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .profile-container {
    position: relative;
  }
  
  .profile-button {
    /* Interactive Design: Clear interaction target */
    background: transparent;
    border: none;
    padding: 0.5rem;
    border-radius: 50%;
    cursor: pointer;
    color: theme.secondary;
    transition: all 250ms ease-out;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .profile-button:hover {
    color: theme.text;
    background: rgba(127, 127, 127, 0.1);
  }
  
  .avatar {
    /* Visual Design: Consistent avatar styling */
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: theme.accent;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
  }
  
  /* Responsive Design: Mobile-first approach */
  @media (max-width: 768px) {
    .header-content {
      grid-template-columns: auto 1fr auto;
      padding: 0 1rem;
      gap: 1rem;
    }
    
    .nav-list {
      display: none; /* Mobile: Collapse navigation */
    }
    
    .logo-text {
      font-size: 1.25rem;
    }
  }
  
  /* Advanced: Reduced motion for accessibility */
  @media (prefers-reduced-motion: reduce) {
    .nav-link,
    .theme-toggle,
    .profile-button {
      transition: none;
    }
    
    .nav-link:hover,
    .theme-toggle:hover,
    .profile-button:hover {
      transform: none;
    }
  }
</style>