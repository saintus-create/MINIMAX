# KokonutUI News Website

A sophisticated news platform featuring Apple's clean Entertainment-inspired design with 12 modern KokonutUI components. Built with Svelte and featuring purposeful animations, three-theme system, and responsive design.

## ✨ Features

### Design Philosophy
- **Apple Entertainment Inspired** - Clean, content-first editorial aesthetic
- **Purposeful Animations** - Every animation serves a clear UX purpose (not random effects)
- **Sophisticated Monochrome Theme** - Black/white extremes with strategic blue accents
- **Three-Theme System** - Light, Dark, and Monochrome themes with smooth transitions

### KokonutUI Components Integrated
- **Bento Grid** - Asymmetric layout system for content organization
- **Liquid Glass Cards** - Premium backdrop blur effects
- **Smooth Tab Navigation** - Sliding indicator with 300ms ease-out timing
- **Action Search Bar** - Purposeful search expansion and cascading results
- **Shapes Hero** - Breaking news with animated background effects
- **Typing Text** - Character-by-character animation for dynamic headlines
- **Beams Background** - Animated gradient beams for visual appeal
- **X Card** - Social sharing integration
- **Mouse Effect Card** - Interactive tilt and spotlight effects
- **Profile Dropdown** - Apple Activity Card inspired user interface
- **Shimmer Text** - Loading state animations
- **Circular Progress** - Reading statistics with SVG animations

### Technical Features
- **Svelte 5** - Modern reactive framework with $state, $derived, $effect runes
- **Responsive Design** - Mobile-first approach with breakpoints at 768px and 1024px
- **Accessibility** - WCAG AAA contrast ratios and reduced motion support
- **Performance Optimized** - GPU-accelerated animations using CSS transforms

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ 
- npm or yarn

### Installation
1. Clone the repository:
```bash
git clone https://github.com/yourusername/kokonutui-news-website.git
cd kokonutui-news-website
```

2. Install dependencies:
```bash
npm install
```

3. Start development server:
```bash
npm run dev
```

4. Open your browser to `http://localhost:5173`

### Build for Production
```bash
npm run build
npm run preview
```

### GitHub Pages Deployment
1. **Push your code to GitHub:**
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/kokonutui-news-website.git
git push -u origin main
```

2. **Enable GitHub Pages:**
   - Go to your repository on GitHub
   - Navigate to **Settings** → **Pages**
   - Under **Source**, select **Deploy from a branch**
   - Choose **main** branch and **/ (root)** folder
   - Click **Save**

3. **Build and Deploy (GitHub Actions):**
   The repository includes automatic deployment via GitHub Actions. Alternatively, you can manually build:
   ```bash
   npm run build
   ```
   Then upload the contents of the `dist/` folder to the root of your repository.

4. **Access your site:**
   Your site will be available at: `https://yourusername.github.io/kokonutui-news-website`

**Note**: The site uses relative paths (`base: './'` in vite.config.js) to work correctly with GitHub Pages subdirectories.

## 🎨 Theme System

The website features three distinct themes:

### Light Theme
- Clean whites and subtle grays
- High contrast for readability
- Perfect for daytime reading

### Dark Theme  
- Rich dark backgrounds
- Reduced eye strain for evening reading
- Maintains visual hierarchy

### Monochrome Theme
- Pure black and white extremes
- Strategic blue accents (#007AFF) for interactive elements
- Sophisticated editorial aesthetic
- Maintains WCAG AAA contrast ratios

## 🔧 Development

### File Structure
```
/
├── App.svelte                 # Main application with theme system
├── components/                # Svelte components
│   ├── Header.svelte         # Navigation with search and profile
│   ├── Hero.svelte           # Breaking news with typing text
│   ├── FeaturedStories.svelte # Bento grid with liquid glass cards
│   ├── NewsCategories.svelte  # Smooth tab navigation
│   ├── TrendingStories.svelte # X card and mouse effects
│   ├── ProfileDropdown.svelte # Apple Activity Card inspired
│   ├── ActionSearchBar.svelte # Purposeful search flow
│   ├── ShimmerText.svelte    # Loading states
│   └── Footer.svelte         # Comprehensive footer
├── package.json              # Dependencies and scripts
├── vite.config.js           # Vite configuration
└── index.html               # HTML entry point
```

### Animation Philosophy
All animations follow a purposeful design:
- **300ms timing** - Consistent across all transitions
- **Easing functions** - Ease-out for natural motion
- **UX purpose** - Guide attention, provide feedback, show hierarchy
- **Performance** - GPU-accelerated transforms
- **Accessibility** - Respects `prefers-reduced-motion`

### Responsive Breakpoints
- **Mobile**: < 768px
- **Tablet**: 768px - 1024px  
- **Desktop**: > 1024px

## 🌟 Design Principles

Based on comprehensive design guidelines including:
- **Gestalt Principles** - Closure, similarity, continuation, common fate, focal point
- **Composition Rules** - Visual hierarchy, whitespace usage, alignment
- **Form & Space** - Balance, proportion, rhythm, contrast
- **Color Theory** - Semantic colors with theme-specific neutrals

## 📱 Browser Support

- Chrome/Edge 88+
- Firefox 85+
- Safari 14+
- Mobile browsers with CSS backdrop-filter support

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- **KokonutUI** - Modern React component library with 250+ components
- **Apple Entertainment** - Design inspiration for clean editorial aesthetic
- **Svelte Team** - Excellent reactive framework
- **Vite** - Fast development tooling

---

Built with ❤️ using Svelte and KokonutUI components