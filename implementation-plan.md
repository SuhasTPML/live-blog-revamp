# Read More/Less Implementation Plan

## Overview
Implement expandable subtitle functionality where clicking "Read More" expands the truncated text to show the full content, and clicking "Read Less" collapses it back to the original state.

## Technical Implementation

### 1. HTML Structure
```html
<div class="article-subtitle">
    <p id="subtitle-text">
        <span class="truncated-text">Iran has dismissed calls for resuming nuclear negotiations with the United States, expressing skepticism over bolstering the nuclear deal, and even diluted the reforms when it seemed as if the fragile order might not hold. Meanwhile, reports suggest that the US...</span>
        <span class="full-text" style="display: none;">Iran has dismissed calls for resuming nuclear negotiations with the United States, expressing skepticism over bolstering the nuclear deal, and even diluted the reforms when it seemed as if the fragile order might not hold. Meanwhile, reports suggest that the US is considering new sanctions as diplomatic efforts continue to stall. Regional tensions have escalated following recent strikes, with multiple countries calling for de-escalation. The international community remains divided on the best approach to address these mounting concerns.</span>
        <a href="#" class="read-more-link" id="readMoreBtn">Read More</a>
    </p>
</div>
```

### 2. CSS Enhancements
```css
.article-subtitle {
    margin-bottom: 20px;
    padding-bottom: 15px;
    border-bottom: 1px solid #eee;
    transition: all 0.3s ease;
}

.full-text {
    display: none;
}

.read-more-link {
    color: #0891b2;
    text-decoration: none;
    font-weight: 500;
    font-size: 14px;
    margin-left: 5px;
    cursor: pointer;
    transition: color 0.2s ease;
}

.read-more-link:hover {
    text-decoration: underline;
}

/* Animation for smooth expansion */
.expanding {
    animation: expandText 0.3s ease-out;
}

@keyframes expandText {
    from { max-height: 3em; overflow: hidden; }
    to { max-height: 20em; overflow: visible; }
}
```

### 3. JavaScript Functionality
```javascript
function initializeReadMore() {
    const readMoreBtn = document.getElementById('readMoreBtn');
    const truncatedText = document.querySelector('.truncated-text');
    const fullText = document.querySelector('.full-text');
    
    let isExpanded = false;
    
    readMoreBtn.addEventListener('click', function(e) {
        e.preventDefault();
        
        if (!isExpanded) {
            // Expand text
            truncatedText.style.display = 'none';
            fullText.style.display = 'inline';
            readMoreBtn.textContent = 'Read Less';
            isExpanded = true;
        } else {
            // Collapse text
            truncatedText.style.display = 'inline';
            fullText.style.display = 'none';
            readMoreBtn.textContent = 'Read More';
            isExpanded = false;
        }
    });
}

// Initialize on page load
document.addEventListener('DOMContentLoaded', initializeReadMore);
```

### 4. Responsive Considerations
- Ensure smooth transitions on mobile devices
- Adjust animation duration for different screen sizes
- Maintain touch-friendly click targets

## Text Wireframes

### Desktop Layout - Default State
```
┌─────────────────────────────────────────────────────────────────────────────┐
│                             ARTICLE HEADER                                  │
│                                                                             │
│ [LIVE] West Asia Tensions LIVE | Iran says no plan for new US nuclear talks│
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │                        ARTICLE SUBTITLE                                 │ │
│ │ Iran has dismissed calls for resuming nuclear negotiations with the    │ │
│ │ United States, expressing skepticism over bolstering the nuclear deal, │ │
│ │ and even diluted the reforms when it seemed as if the fragile order    │ │
│ │ might not hold. Meanwhile, reports suggest that the US... Read More     │ │
│ │                                                        ─────────        │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │ [DH] DH Web Desk                                                        │ │
│ │      Last Updated: 2 hours ago                                          │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
│ ─────────────────────────────────────────────────────────────────────────── │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │ Follow Us [f] [t] [W] [T]                                               │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────┘
│                                                                             │
┌─────────────────────────────────────────────────────────────────────────────┐
│                             HERO IMAGE                                     │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │                                                                         │ │
│ │                    [Article Image Placeholder]                         │ │
│ │                                                                         │ │
│ │ Caption: A satellite image shows sensitive content over the underground │ │
│ │ enrichment halls of the Natanz Enrichment Facility. Credit: Reuters    │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────┘
│                                                                             │
┌─────────────────────────────────────────────────────────────────────────────┐
│                           CONTEXT PARAGRAPHS                               │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │                         PARAGRAPH 1                                    │ │
│ │ The ongoing tensions in West Asia have reached a critical juncture as  │ │
│ │ diplomatic efforts to revive the nuclear agreement face mounting       │ │
│ │ challenges. Iran's rejection of new talks comes amid escalating...     │ │
│ │ Read More                                                               │ │
│ │ ─────────                                                               │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │                         PARAGRAPH 2                                    │ │
│ │ (Hidden - shows after clicking Read More)                              │ │
│ │ Regional powers including Saudi Arabia, UAE, and Israel have expressed │ │
│ │ concerns about Iran's nuclear program advancement. Recent satellite     │ │
│ │ imagery suggests continued enrichment activities at key facilities...   │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │                         PARAGRAPH 3                                    │ │
│ │ (Hidden - shows after clicking Read More)                              │ │
│ │ The economic implications of the current standoff extend far beyond    │ │
│ │ the region, with global oil markets showing increased volatility and   │ │
│ │ shipping routes through the Persian Gulf facing potential disruption... │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────┘
│                                                                             │
┌─────────────────────────────────────────────────────────────────────────────┐
│                        KEY UPDATES TIMELINE                                │
│                        (Horizontal Scrolling)                              │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │ ← [Jul 17, 04:46] Iran says no plan → [Jul 17, 04:37] A planned loss → [Jul 17, 04:32] US people│ │
│ │   for new US nuclear talks        from armaments future      arrested in Iran │ │
│ │                                                                         │ │
│ │ → [Jul 17, 04:20] Prominent Indian nationals from Iraq                 │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────┘
│                                                                             │
┌─────────────────────────────────────────────────────────────────────────────┐
│                            LIVE UPDATES                                    │
│                                                                             │
│ ┌─────────────────────────────────────────────────────────────────────────┐ │
│ │ │ [Jul 17, 04:46 PM] West Asia Tensions LIVE | Iran says no plan for new...    │ │
│ │ │ Iran says it has no plan for new nuclear negotiations...             │ │
│ │ │ [KEY UPDATE]                                                          │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 04:37 PM] West Asia Tensions LIVE | A planned loss from...          │ │
│ │ │ Reports from government ministries suggest...                        │ │
│ │ │ [KEY UPDATE]                                                          │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 04:32 PM] West Asia Tensions LIVE | US people arrested...           │ │
│ │ │ Iran media reports suggest multiple arrests...                       │ │
│ │ │ [KEY UPDATE]                                                          │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 04:20 PM] West Asia Tensions LIVE | Prominent Indian nationals...   │ │
│ │ │ Reports indicate several Indian nationals have been evacuated...     │ │
│ │ │ [KEY UPDATE]                                                          │ │
│ │                                                                         │ │
│ │ │ Indian embassy sources confirm that prominent Indian nationals        │ │
│ │ │ working in Iraq have been safely evacuated following escalating      │ │
│ │ │ security concerns. The evacuation was coordinated with local          │ │
│ │ │ authorities and represents a precautionary measure amid regional      │ │
│ │ │ instability affecting civilian populations.                           │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 04:15 PM] West Asia Tensions LIVE | Iran announces new framework... │ │
│ │ │ Iranian officials outline revised approach to nuclear talks...       │ │
│ │                                                                         │ │
│ │ │ Senior Iranian diplomats have presented a new framework for           │ │
│ │ │ potential nuclear negotiations, emphasizing pre-conditions and        │ │
│ │ │ guarantees before any formal talks can commence. The proposal         │ │
│ │ │ includes specific demands for sanctions relief and security           │ │
│ │ │ assurances from Western powers.                                       │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 04:10 PM] West Asia Tensions LIVE | Iran reiterates nuclear stance  │ │
│ │ │ Officials maintain consistent position on nuclear program...          │ │
│ │                                                                         │ │
│ │ │ Iranian leadership has reiterated their firm stance on nuclear        │ │
│ │ │ development rights, emphasizing that any international agreements     │ │
│ │ │ must respect Iran's sovereignty and technological advancement          │ │
│ │ │ capabilities. The statement comes as international pressure           │ │
│ │ │ continues to mount from various diplomatic channels.                  │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 04:05 PM] West Asia Tensions LIVE | Iran-IAEA cooperation update    │ │
│ │ │ New developments in Iran's cooperation with nuclear watchdog...       │ │
│ │                                                                         │ │
│ │ │ The International Atomic Energy Agency has received updated           │ │
│ │ │ commitments from Iran regarding inspection protocols and monitoring   │ │
│ │ │ access to nuclear facilities. However, implementation details        │ │
│ │ │ remain under negotiation, with both sides working to establish       │ │
│ │ │ mutually acceptable terms for enhanced cooperation.                   │ │
│ │                                                                         │ │
│ │ │ [Jul 17, 03:58 PM] West Asia Tensions LIVE | Regional damage assessment      │ │
│ │ │ Iran urges assessment of regional damage from ongoing conflicts...    │ │
│ │                                                                         │ │
│ │ │ Iranian foreign ministry officials have called for a comprehensive    │ │
│ │ │ assessment of regional damage caused by ongoing conflicts, citing     │ │
│ │ │ humanitarian concerns and economic disruption across West Asia.       │ │
│ │ │ The statement emphasizes the need for coordinated international       │ │
│ │ │ response to address civilian casualties and infrastructure damage.    │ │
│ └─────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────┘
```

## Implementation Steps

### Phase 1: HTML Structure Update
1. Split subtitle text into truncated and full versions
2. Add unique IDs for JavaScript targeting
3. Wrap content in appropriate containers

### Phase 2: CSS Enhancements
1. Add transition effects for smooth expansion
2. Ensure responsive behavior is maintained
3. Style the read more/less link states

### Phase 3: JavaScript Implementation
1. Create toggle function for expand/collapse
2. Add event listeners for click handling
3. Implement smooth animations
4. Test cross-browser compatibility

### Phase 4: Testing & Optimization
1. Test on various screen sizes
2. Verify accessibility compliance
3. Optimize performance for mobile devices
4. Test with different content lengths

## Key Features

### Functionality
- ✅ Click "Read More" to expand text
- ✅ Click "Read Less" to collapse text
- ✅ Smooth animations between states
- ✅ Responsive behavior on all devices
- ✅ Maintains inline link positioning

### User Experience
- ✅ Clear visual indication of expandable content
- ✅ Consistent interaction patterns
- ✅ Touch-friendly on mobile devices
- ✅ Accessible keyboard navigation
- ✅ Smooth transitions for better UX

### Technical Considerations
- ✅ Vanilla JavaScript (no dependencies)
- ✅ CSS3 transitions for smooth animations
- ✅ Responsive design compatibility
- ✅ Cross-browser support
- ✅ Performance optimized

## File Structure After Implementation
```
liveblog/
├── index.html          # Updated with expandable subtitle
├── README.md          # Updated documentation
└── implementation-plan.md  # This file
```

## Success Metrics
- Users can successfully expand/collapse subtitle text
- Smooth animations work across all devices
- No layout shifts or jumping during transitions
- Accessible to screen readers and keyboard users
- Performance remains optimal on mobile devices
