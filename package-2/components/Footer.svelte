<script>
  export let theme = {};
  
  // Footer with comprehensive navigation - Apple Entertainment inspired
  const footerSections = [
    {
      title: 'News & Media',
      links: [
        { name: 'Latest News', href: '#' },
        { name: 'Breaking News', href: '#' },
        { name: 'Investigative', href: '#' },
        { name: 'Opinion', href: '#' },
        { name: 'Photojournalism', href: '#' },
        { name: 'Video', href: '#' }
      ]
    },
    {
      title: 'Categories',
      links: [
        { name: 'World', href: '#' },
        { name: 'Politics', href: '#' },
        { name: 'Technology', href: '#' },
        { name: 'Science', href: '#' },
        { name: 'Health', href: '#' },
        { name: 'Sports', href: '#' },
        { name: 'Entertainment', href: '#' },
        { name: 'Business', href: '#' }
      ]
    },
    {
      title: 'Services',
      links: [
        { name: 'Newsletters', href: '#' },
        { name: 'Podcasts', href: '#' },
        { name: 'Mobile App', href: '#' },
        { name: 'RSS Feeds', href: '#' },
        { name: 'API Access', href: '#' },
        { name: 'Archive', href: '#' }
      ]
    },
    {
      title: 'Company',
      links: [
        { name: 'About Us', href: '#' },
        { name: 'Careers', href: '#' },
        { name: 'Contact', href: '#' },
        { name: 'Press', href: '#' },
        { name: 'Advertise', href: '#' },
        { name: 'Partnerships', href: '#' }
      ]
    },
    {
      title: 'Legal',
      links: [
        { name: 'Privacy Policy', href: '#' },
        { name: 'Terms of Service', href: '#' },
        { name: 'Cookie Policy', href: '#' },
        { name: 'Accessibility', href: '#' },
        { name: 'Corrections', href: '#' },
        { name: 'Ethics Policy', href: '#' }
      ]
    }
  ];
  
  const socialLinks = [
    {
      name: 'Twitter',
      href: '#',
      icon: '<path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"/>'
    },
    {
      name: 'Facebook',
      href: '#',
      icon: '<path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>'
    },
    {
      name: 'Instagram',
      href: '#',
      icon: '<rect x="2" y="2" width="20" height="20" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/>'
    },
    {
      name: 'LinkedIn',
      href: '#',
      icon: '<path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/>'
    },
    {
      name: 'YouTube',
      href: '#',
      icon: '<path d="M22.46 6c-.77.35-1.6.58-2.46.69.88-.53 1.56-1.37 1.88-2.38-.83.5-1.75.85-2.72 1.05C18.37 4.5 17.26 4 16 4c-2.35 0-4.27 1.92-4.27 4.29 0 .34.04.67.11.98C8.28 9.09 5.11 7.38 3 4.79c-.37.63-.58 1.37-.58 2.15 0 1.49.75 2.81 1.91 3.56-.71 0-1.37-.2-1.95-.5v.03c0 2.08 1.48 3.82 3.44 4.21a4.22 4.22 0 0 1-1.93.07 4.28 4.28 0 0 0 4 2.98 8.521 8.521 0 0 1-5.33 1.84c-.34 0-.68-.02-1.02-.06C3.44 20.29 5.7 21 8.12 21 16 21 20.33 14.46 20.33 8.79c0-.19 0-.37-.01-.56.84-.6 1.56-1.36 2.14-2.23z"/>'
    }
  ];
  
  const currentYear = new Date().getFullYear();
</script>

<footer class="footer">
  <div class="footer-content">
    <!-- Main Footer Navigation -->
    <div class="footer-navigation">
      {#each footerSections as section, index}
        <div 
          class="footer-section"
          style="animation-delay: {index * 100}ms;"
        >
          <h3 class="section-title">{section.title}</h3>
          <ul class="section-links">
            {#each section.links as link}
              <li>
                <a href={link.href} class="footer-link">
                  {link.name}
                </a>
              </li>
            {/each}
          </ul>
        </div>
      {/each}
    </div>
    
    <!-- Newsletter Signup -->
    <div class="newsletter-section">
      <div class="newsletter-content">
        <h3 class="newsletter-title">Stay Informed</h3>
        <p class="newsletter-description">
          Get the latest news delivered directly to your inbox with our daily newsletter.
        </p>
        <form class="newsletter-form">
          <div class="form-group">
            <input 
              type="email" 
              placeholder="Enter your email address"
              class="email-input"
              required
            />
            <button type="submit" class="subscribe-button">
              Subscribe
            </button>
          </div>
          <p class="newsletter-disclaimer">
            By subscribing, you agree to our Privacy Policy and consent to receive updates.
          </p>
        </form>
      </div>
    </div>
  </div>
  
  <!-- Footer Bottom -->
  <div class="footer-bottom">
    <div class="footer-bottom-content">
      <!-- Brand Section -->
      <div class="brand-section">
        <div class="logo">
          <h2 class="logo-text">NewsHub</h2>
        </div>
        <p class="brand-description">
          Your trusted source for breaking news, in-depth analysis, and expert commentary 
          from around the world.
        </p>
      </div>
      
      <!-- Social Media -->
      <div class="social-section">
        <h4 class="social-title">Follow Us</h4>
        <div class="social-links">
          {#each socialLinks as social, index}
            <a 
              href={social.href}
              class="social-link"
              aria-label="Follow us on {social.name}"
              style="animation-delay: {index * 50}ms;"
            >
              <div class="social-icon">
                {@html social.icon}
              </div>
            </a>
          {/each}
        </div>
      </div>
    </div>
    
    <!-- Copyright and Legal -->
    <div class="copyright-section">
      <div class="copyright-content">
        <p class="copyright-text">
          © {currentYear} NewsHub. All rights reserved.
        </p>
        <div class="legal-links">
          <a href="#" class="legal-link">Privacy</a>
          <a href="#" class="legal-link">Terms</a>
          <a href="#" class="legal-link">Cookies</a>
          <a href="#" class="legal-link">Accessibility</a>
        </div>
      </div>
    </div>
  </div>
</footer>

<style>
  .footer {
    /* Foundation: Footer background and layout */
    background: linear-gradient(135deg, 
      theme.surface 0%, 
      rgba(127, 127, 127, 0.05) 100%);
    border-top: 1px solid rgba(127, 127, 127, 0.1);
    margin-top: 4rem;
    
    /* Layout: Comprehensive footer structure */
  }
  
  .footer-content {
    /* Layout: Main footer content */
    max-width: 1400px;
    margin: 0 auto;
    padding: 4rem 2rem 2rem;
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 4rem;
  }
  
  .footer-navigation {
    /* Layout: Footer navigation grid */
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
  }
  
  .footer-section {
    /* Layout: Individual footer section */
    animation: fadeInUp 0.6s ease-out forwards;
    opacity: 0;
    transform: translateY(20px);
  }
  
  .section-title {
    /* Typography: Section titles */
    font-size: 1rem;
    font-weight: 600;
    color: theme.text;
    margin: 0 0 1rem 0;
    letter-spacing: 0.025em;
  }
  
  .section-links {
    /* Layout: Links list */
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  
  .footer-link {
    /* Interactive: Footer links */
    color: theme.secondary;
    text-decoration: none;
    font-size: 0.875rem;
    transition: color 200ms ease-out;
  }
  
  .footer-link:hover {
    /* Feedback: Hover state */
    color: theme.accent;
  }
  
  .newsletter-section {
    /* Layout: Newsletter signup */
  }
  
  .newsletter-content {
    /* Layout: Newsletter content area */
    background: theme.surface;
    padding: 2rem;
    border-radius: 1rem;
    border: 1px solid rgba(127, 127, 127, 0.1);
  }
  
  .newsletter-title {
    /* Typography: Newsletter title */
    font-size: 1.25rem;
    font-weight: 600;
    color: theme.text;
    margin: 0 0 0.5rem 0;
  }
  
  .newsletter-description {
    /* Typography: Newsletter description */
    font-size: 0.875rem;
    color: theme.secondary;
    line-height: 1.5;
    margin: 0 0 1.5rem 0;
  }
  
  .newsletter-form {
    /* Layout: Newsletter form */
  }
  
  .form-group {
    /* Layout: Form input and button */
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
  }
  
  .email-input {
    /* Typography: Email input styling */
    flex: 1;
    padding: 0.75rem 1rem;
    border: 1px solid rgba(127, 127, 127, 0.3);
    border-radius: 0.5rem;
    background: theme.bg;
    color: theme.text;
    font-size: 0.875rem;
    transition: border-color 200ms ease-out;
  }
  
  .email-input:focus {
    /* Focus: Border highlight */
    outline: none;
    border-color: theme.accent;
    box-shadow: 0 0 0 3px rgba(0, 122, 255, 0.1);
  }
  
  .subscribe-button {
    /* Interactive: Subscribe button */
    background: theme.accent;
    color: white;
    border: none;
    padding: 0.75rem 1.5rem;
    border-radius: 0.5rem;
    font-weight: 500;
    font-size: 0.875rem;
    cursor: pointer;
    transition: all 250ms ease-out;
    white-space: nowrap;
  }
  
  .subscribe-button:hover {
    /* Motion: Purposeful hover feedback */
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(0, 122, 255, 0.3);
  }
  
  .newsletter-disclaimer {
    /* Typography: Disclaimer text */
    font-size: 0.75rem;
    color: theme.secondary;
    line-height: 1.4;
    margin: 0;
  }
  
  .footer-bottom {
    /* Layout: Footer bottom section */
    border-top: 1px solid rgba(127, 127, 127, 0.1);
    background: rgba(127, 127, 127, 0.02);
  }
  
  .footer-bottom-content {
    /* Layout: Footer bottom content */
    max-width: 1400px;
    margin: 0 auto;
    padding: 2rem;
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 2rem;
    align-items: start;
  }
  
  .brand-section {
    /* Layout: Brand information */
  }
  
  .logo-text {
    /* Typography: Logo styling */
    font-size: 1.5rem;
    font-weight: 700;
    color: theme.text;
    margin: 0 0 0.5rem 0;
    letter-spacing: -0.025em;
  }
  
  .brand-description {
    /* Typography: Brand description */
    font-size: 0.875rem;
    color: theme.secondary;
    line-height: 1.6;
    margin: 0;
    max-width: 400px;
  }
  
  .social-section {
    /* Layout: Social media section */
  }
  
  .social-title {
    /* Typography: Social section title */
    font-size: 1rem;
    font-weight: 600;
    color: theme.text;
    margin: 0 0 1rem 0;
  }
  
  .social-links {
    /* Layout: Social links grid */
    display: flex;
    gap: 0.75rem;
  }
  
  .social-link {
    /* Interactive: Social link buttons */
    width: 40px;
    height: 40px;
    background: theme.surface;
    border: 1px solid rgba(127, 127, 127, 0.2);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: theme.secondary;
    text-decoration: none;
    transition: all 250ms ease-out;
    animation: fadeInScale 0.4s ease-out forwards;
    opacity: 0;
    transform: scale(0.8);
  }
  
  .social-link:hover {
    /* Feedback: Hover state */
    color: theme.accent;
    border-color: theme.accent;
    transform: scale(1.1);
  }
  
  .social-icon {
    /* Visual: Social icons */
    width: 18px;
    height: 18px;
  }
  
  .social-icon :global(svg) {
    width: 100%;
    height: 100%;
  }
  
  .copyright-section {
    /* Layout: Copyright section */
    border-top: 1px solid rgba(127, 127, 127, 0.1);
    background: rgba(127, 127, 127, 0.05);
  }
  
  .copyright-content {
    /* Layout: Copyright content */
    max-width: 1400px;
    margin: 0 auto;
    padding: 1.5rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
  }
  
  .copyright-text {
    /* Typography: Copyright text */
    font-size: 0.875rem;
    color: theme.secondary;
    margin: 0;
  }
  
  .legal-links {
    /* Layout: Legal links */
    display: flex;
    gap: 1.5rem;
  }
  
  .legal-link {
    /* Interactive: Legal links */
    color: theme.secondary;
    text-decoration: none;
    font-size: 0.875rem;
    transition: color 200ms ease-out;
  }
  
  .legal-link:hover {
    color: theme.accent;
  }
  
  /* Keyframe Animations */
  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  @keyframes fadeInScale {
    to {
      opacity: 1;
      transform: scale(1);
    }
  }
  
  /* Responsive Design */
  @media (max-width: 1024px) {
    .footer-content,
    .footer-bottom-content {
      grid-template-columns: 1fr;
      gap: 3rem;
    }
    
    .footer-navigation {
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    }
  }
  
  @media (max-width: 768px) {
    .footer-content {
      padding: 3rem 1rem 2rem;
    }
    
    .footer-navigation {
      grid-template-columns: 1fr;
      gap: 2rem;
    }
    
    .newsletter-content {
      padding: 1.5rem;
    }
    
    .form-group {
      flex-direction: column;
    }
    
    .email-input,
    .subscribe-button {
      width: 100%;
    }
    
    .footer-bottom-content {
      padding: 1.5rem 1rem;
      text-align: center;
    }
    
    .copyright-content {
      flex-direction: column;
      text-align: center;
      padding: 1.5rem 1rem;
    }
    
    .legal-links {
      justify-content: center;
    }
  }
  
  /* Accessibility: Reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .footer-section,
    .social-link {
      animation: none;
    }
    
    .footer-section {
      opacity: 1;
      transform: none;
    }
    
    .social-link {
      opacity: 1;
      transform: none;
    }
    
    .footer-link:hover,
    .subscribe-button:hover,
    .social-link:hover {
      transform: none;
    }
  }
</style>