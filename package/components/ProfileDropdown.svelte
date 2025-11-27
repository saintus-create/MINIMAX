<script>
  import { onMount } from 'svelte';
  
  export let onClose = () => {};
  export let theme = {};
  
  // User data - in real app would come from authentication system
  const user = {
    name: 'Alex Thompson',
    email: 'alex.thompson@email.com',
    avatar: 'AT',
    role: 'Premium Subscriber'
  };
  
  // Menu items with hierarchical organization
  const menuItems = [
    {
      section: 'Account',
      items: [
        { icon: 'user', label: 'Profile', action: 'profile' },
        { icon: 'settings', label: 'Settings', action: 'settings' },
        { icon: 'bookmark', label: 'Saved Articles', action: 'bookmarks' },
        { icon: 'history', label: 'Reading History', action: 'history' }
      ]
    },
    {
      section: 'Preferences', 
      items: [
        { icon: 'bell', label: 'Notifications', action: 'notifications' },
        { icon: 'palette', label: 'Themes', action: 'themes' },
        { icon: 'language', label: 'Language', action: 'language' }
      ]
    },
    {
      section: 'Support',
      items: [
        { icon: 'help', label: 'Help & Support', action: 'help' },
        { icon: 'feedback', label: 'Send Feedback', action: 'feedback' }
      ]
    }
  ];
  
  // User reading statistics - Apple Activity Card inspired
  const readingStats = {
    articlesRead: 47,
    weeklyGoal: 50,
    streak: 12,
    favoriteCategory: 'Technology'
  };
  
  function handleMenuClick(action) {
    // In real app: Navigate to appropriate section or perform action
    console.log(`Action: ${action}`);
    onClose();
  }
  
  function handleSignOut() {
    // In real app: Handle sign out logic
    console.log('Sign out');
    onClose();
  }
  
  // Calculate reading progress percentage
  $: progressPercentage = Math.min((readingStats.articlesRead / readingStats.weeklyGoal) * 100, 100);
  
  // Click outside to close
  onMount(() => {
    function handleClickOutside(event) {
      if (!event.target.closest('.profile-dropdown')) {
        onClose();
      }
    }
    
    // Small delay to prevent immediate close on click
    setTimeout(() => {
      document.addEventListener('click', handleClickOutside);
    }, 100);
    
    return () => document.removeEventListener('click', handleClickOutside);
  });
</script>

<div class="profile-dropdown" transition:scale={{ duration: 200, start: 0.95 }}>
  <!-- User Info Section -->
  <div class="user-section">
    <div class="user-avatar">
      <span class="avatar-text">{user.avatar}</span>
    </div>
    <div class="user-info">
      <div class="user-name">{user.name}</div>
      <div class="user-email">{user.email}</div>
      <div class="user-role">{user.role}</div>
    </div>
  </div>
  
  <!-- Reading Statistics - Apple Activity Card Style -->
  <div class="stats-section">
    <div class="stats-header">
      <h4 class="stats-title">Reading Progress</h4>
      <div class="stats-goal">{readingStats.articlesRead}/{readingStats.weeklyGoal}</div>
    </div>
    
    <div class="progress-container">
      <!-- Circular progress indicator -->
      <div class="circular-progress">
        <svg width="60" height="60" class="progress-ring">
          <circle
            cx="30"
            cy="30"
            r="25"
            fill="transparent"
            stroke="rgba(127, 127, 127, 0.2)"
            stroke-width="3"
          />
          <circle
            cx="30"
            cy="30"
            r="25"
            fill="transparent"
            stroke="theme.accent"
            stroke-width="3"
            stroke-linecap="round"
            stroke-dasharray={`${2 * Math.PI * 25}`}
            stroke-dashoffset={`${2 * Math.PI * 25 * (1 - progressPercentage / 100)}`}
            class="progress-circle"
          />
        </svg>
        <div class="progress-text">
          <div class="progress-number">{Math.round(progressPercentage)}%</div>
          <div class="progress-label">Complete</div>
        </div>
      </div>
      
      <div class="stats-details">
        <div class="stat-item">
          <div class="stat-icon streak">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
            </svg>
          </div>
          <div class="stat-text">
            <div class="stat-value">{readingStats.streak} day streak</div>
            <div class="stat-label">Reading streak</div>
          </div>
        </div>
        
        <div class="stat-item">
          <div class="stat-icon category">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
          </div>
          <div class="stat-text">
            <div class="stat-value">{readingStats.favoriteCategory}</div>
            <div class="stat-label">Favorite category</div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <!-- Menu Sections -->
  {#each menuItems as section, sectionIndex}
    <div class="menu-section">
      <h5 class="section-title">{section.section}</h5>
      <div class="menu-items">
        {#each section.items as item, itemIndex}
          <button 
            class="menu-item"
            on:click={() => handleMenuClick(item.action)}
            style="animation-delay: {(sectionIndex * 100) + (itemIndex * 50)}ms;"
          >
            <div class="menu-icon">
              {#if item.icon === 'user'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/>
                  <circle cx="12" cy="7" r="4"/>
                </svg>
              {:else if item.icon === 'settings'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="3"/>
                  <path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"/>
                </svg>
              {:else if item.icon === 'bookmark'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M19 21l-7-5-7 5V5a2 2 0 0 1 2-2h10a2 2 0 0 1 2 2z"/>
                </svg>
              {:else if item.icon === 'history'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M3 3v5h5"/>
                  <path d="M3.05 13A9 9 0 1 0 6 5.3L3 8"/>
                  <path d="M12 7v5l3 3"/>
                </svg>
              {:else if item.icon === 'bell'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/>
                  <path d="M13.73 21a2 2 0 0 1-3.46 0"/>
                </svg>
              {:else if item.icon === 'palette'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="13.5" cy="6.5" r=".5"/>
                  <circle cx="17.5" cy="10.5" r=".5"/>
                  <circle cx="8.5" cy="7.5" r=".5"/>
                  <circle cx="6.5" cy="12.5" r=".5"/>
                  <path d="M12 2C6.5 2 2 6.5 2 12s4.5 10 10 10c.926 0 1.648-.746 1.648-1.688 0-.437-.18-.835-.437-1.125-.29-.289-.438-.652-.438-1.125a1.64 1.64 0 0 1 1.668-1.668h1.996c3.051 0 5.555-2.503 5.555-5.554C21.965 6.012 17.461 2 12 2z"/>
                </svg>
              {:else if item.icon === 'language'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M12 2a10 10 0 0 0 0 20 10 10 0 0 0 0-20z"/>
                  <path d="M2 12h20"/>
                  <path d="M12 2c15 3 1 18 1 18s-4-2-5-5 2-6 2-6 4 2 4 5 2 6 2 6 1 15-1 18-20 3-20-3-20-3 2-15 1-18 1-18 4 2 5 5-2 6-2 6-4-2-4-5-2-6-2-6z"/>
                </svg>
              {:else if item.icon === 'help'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="10"/>
                  <path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"/>
                  <line x1="12" y1="17" x2="12.01" y2="17"/>
                </svg>
              {:else if item.icon === 'feedback'}
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
                </svg>
              {/if}
            </div>
            <span class="menu-label">{item.label}</span>
          </button>
        {/each}
      </div>
    </div>
  {/each}
  
  <!-- Sign Out Section -->
  <div class="sign-out-section">
    <button class="sign-out-button" on:click={handleSignOut}>
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/>
        <polyline points="16,17 21,12 16,7"/>
        <line x1="21" y1="12" x2="9" y2="12"/>
      </svg>
      <span>Sign Out</span>
    </button>
  </div>
</div>

<style>
  .profile-dropdown {
    /* Layout: Dropdown positioning and styling */
    position: absolute;
    top: 100%;
    right: 0;
    margin-top: 0.5rem;
    width: 320px;
    background: theme.surface;
    border: 1px solid rgba(127, 127, 127, 0.2);
    border-radius: 1rem;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    overflow: hidden;
    z-index: 1000;
    
    /* Animation: Scale entrance */
    transform-origin: top right;
  }
  
  /* Animation for scale transition */
  @keyframes scaleIn {
    from {
      opacity: 0;
      transform: scale(0.95) translateY(-10px);
    }
    to {
      opacity: 1;
      transform: scale(1) translateY(0);
    }
  }
  
  .user-section {
    /* Layout: User information header */
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1.5rem;
    border-bottom: 1px solid rgba(127, 127, 127, 0.1);
  }
  
  .user-avatar {
    /* Visual: Avatar styling */
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: theme.accent;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: 600;
    font-size: 1.125rem;
  }
  
  .user-info {
    /* Typography: User details */
    flex: 1;
  }
  
  .user-name {
    font-size: 1rem;
    font-weight: 600;
    color: theme.text;
    margin-bottom: 0.25rem;
  }
  
  .user-email {
    font-size: 0.875rem;
    color: theme.secondary;
    margin-bottom: 0.25rem;
  }
  
  .user-role {
    font-size: 0.75rem;
    color: theme.accent;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }
  
  .stats-section {
    /* Layout: Reading statistics */
    padding: 1.5rem;
    border-bottom: 1px solid rgba(127, 127, 127, 0.1);
  }
  
  .stats-header {
    /* Layout: Stats header */
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }
  
  .stats-title {
    font-size: 0.875rem;
    font-weight: 600;
    color: theme.text;
    margin: 0;
  }
  
  .stats-goal {
    font-size: 0.875rem;
    font-weight: 500;
    color: theme.secondary;
  }
  
  .progress-container {
    /* Layout: Progress display */
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  
  .circular-progress {
    /* Visual: Circular progress indicator */
    position: relative;
    width: 60px;
    height: 60px;
  }
  
  .progress-ring {
    /* Transform for stroke animation */
    transform: rotate(-90deg);
  }
  
  .progress-circle {
    /* Animation: Progress stroke */
    transition: stroke-dashoffset 500ms ease-out;
  }
  
  .progress-text {
    /* Layout: Progress text overlay */
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
  }
  
  .progress-number {
    font-size: 0.75rem;
    font-weight: 600;
    color: theme.text;
    line-height: 1;
  }
  
  .progress-label {
    font-size: 0.625rem;
    color: theme.secondary;
    line-height: 1;
  }
  
  .stats-details {
    /* Layout: Additional stats */
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  
  .stat-item {
    /* Layout: Individual stat item */
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }
  
  .stat-icon {
    /* Visual: Icon styling */
    width: 32px;
    height: 32px;
    border-radius: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
  }
  
  .stat-icon.streak {
    background: #FF9500;
  }
  
  .stat-icon.category {
    background: #34C759;
  }
  
  .stat-text {
    /* Typography: Stat text */
  }
  
  .stat-value {
    font-size: 0.875rem;
    font-weight: 500;
    color: theme.text;
    line-height: 1.2;
  }
  
  .stat-label {
    font-size: 0.75rem;
    color: theme.secondary;
    line-height: 1.2;
  }
  
  .menu-section {
    /* Layout: Menu section organization */
    padding: 1rem 1.5rem 0.5rem;
  }
  
  .section-title {
    /* Typography: Section headers */
    font-size: 0.75rem;
    font-weight: 600;
    color: theme.secondary;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin: 0 0 0.75rem 0;
  }
  
  .menu-items {
    /* Layout: Menu items container */
    display: flex;
    flex-direction: column;
  }
  
  .menu-item {
    /* Interactive: Menu item styling */
    display: flex;
    align-items: center;
    gap: 0.75rem;
    background: transparent;
    border: none;
    padding: 0.75rem;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: background-color 200ms ease-out;
    text-align: left;
    color: theme.text;
    font-size: 0.875rem;
    
    /* Motion: Staggered appearance */
    animation: fadeInLeft 300ms ease-out forwards;
    opacity: 0;
    transform: translateX(-10px);
  }
  
  .menu-item:hover {
    /* Feedback: Hover state */
    background: rgba(127, 127, 127, 0.1);
  }
  
  @keyframes fadeInLeft {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }
  
  .menu-icon {
    /* Visual: Menu icons */
    color: theme.secondary;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    flex-shrink: 0;
  }
  
  .menu-label {
    /* Typography: Menu labels */
    flex: 1;
  }
  
  .sign-out-section {
    /* Layout: Sign out section */
    padding: 1rem 1.5rem;
    border-top: 1px solid rgba(127, 127, 127, 0.1);
  }
  
  .sign-out-button {
    /* Interactive: Sign out button */
    display: flex;
    align-items: center;
    gap: 0.75rem;
    background: transparent;
    border: none;
    padding: 0.75rem;
    border-radius: 0.5rem;
    cursor: pointer;
    color: #FF3B30;
    font-size: 0.875rem;
    font-weight: 500;
    transition: background-color 200ms ease-out;
    width: 100%;
    text-align: left;
  }
  
  .sign-out-button:hover {
    /* Feedback: Hover state */
    background: rgba(255, 59, 48, 0.1);
  }
  
  /* Responsive Design */
  @media (max-width: 768px) {
    .profile-dropdown {
      width: 280px;
      right: -20px; /* Adjust for mobile viewport */
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .menu-item,
    .profile-dropdown {
      animation: none;
    }
    
    .menu-item {
      opacity: 1;
      transform: none;
    }
    
    .progress-circle {
      transition: none;
    }
  }
</style>