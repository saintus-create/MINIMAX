<script>
  import { onMount } from 'svelte';
  import Header from './components/Header.svelte';
  import Hero from './components/Hero.svelte';
  import FeaturedStories from './components/FeaturedStories.svelte';
  import NewsCategories from './components/NewsCategories.svelte';
  import TrendingStories from './components/TrendingStories.svelte';
  import Footer from './components/Footer.svelte';
  
  // Apply design token system based on our visual principles
  // Foundation: Layout, Proximity, Hierarchy, Contrast, Alignment
  let currentTheme = 'light';
  let isDarkMode = false;
  
  const themes = {
    light: {
      bg: '#FFFFFF',
      surface: '#F7F7F7', 
      text: '#1C1C1E',
      secondary: '#636366',
      accent: '#007AFF'
    },
    dark: {
      bg: '#000000',
      surface: '#1C1C1E',
      text: '#E5E5E7', 
      secondary: '#8E8E93',
      accent: '#007AFF'
    },
    monochrome: {
      bg: '#FFFFFF',
      surface: 'rgba(245, 245, 247, 0.6)',
      text: '#000000',
      secondary: '#636366', 
      accent: '#007AFF'
    }
  };
  
  function toggleTheme() {
    const themeKeys = Object.keys(themes);
    const currentIndex = themeKeys.indexOf(currentTheme);
    const nextIndex = (currentIndex + 1) % themeKeys.length;
    currentTheme = themeKeys[nextIndex];
    isDarkMode = currentTheme === 'dark';
  }
  
  onMount(() => {
    // System for managing theme transitions
    document.documentElement.style.setProperty('--theme-transition', '300ms ease-out');
  });
  
  $: theme = themes[currentTheme];
</script>

<div 
  class="app"
  style="background-color: {theme.bg}; color: {theme.text};"
  transition:fade
>
  <Header 
    {currentTheme} 
    {toggleTheme} 
    theme={theme}
  />
  
  <Hero theme={theme} />
  
  <FeaturedStories theme={theme} />
  
  <NewsCategories theme={theme} />
  
  <TrendingStories theme={theme} />
  
  <Footer theme={theme} />
</div>

<style>
  .app {
    min-height: 100vh;
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    transition: background-color 300ms ease-out, color 300ms ease-out;
    /* Technical: Pixel precision, Anti-aliasing */
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  
  /* Foundation Principles: White Space, Layout */
  * {
    box-sizing: border-box;
  }
  
  body {
    margin: 0;
    padding: 0;
    line-height: 1.7;
    /* Typography: Readability, Legibility */
    font-size: 16px;
  }
</style>