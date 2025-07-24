# PACED Assessment Widget Integration

This widget can be easily integrated into any existing web infrastructure.

## Quick Integration

### 1. Include the JavaScript file
```html
<script src="paced-assessment-widget.js"></script>
```

### 2. Create a container
```html
<div id="my-assessment-container"></div>
```

### 3. Initialize the widget
```javascript
const widget = new PACEDAssessmentWidget('my-assessment-container', {
    onComplete: function(data) {
        // Handle completed assessment data
        console.log('Assessment results:', data);
        
        // Send to your backend
        fetch('/api/save-assessment', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(data)
        });
    }
});
```

## Integration Options

### Option 1: Direct HTML Integration
Simply include the JavaScript file and initialize the widget in any HTML page.

### Option 2: WordPress Integration
1. Upload `paced-assessment-widget.js` to your theme's assets folder
2. Enqueue the script in your theme's functions.php
3. Add the container div and initialization script to any page/post

### Option 3: React/Vue Integration
```javascript
// React example
import { useEffect, useRef } from 'react';

function PACEDAssessment() {
    const containerRef = useRef();
    
    useEffect(() => {
        if (window.PACEDAssessmentWidget) {
            new window.PACEDAssessmentWidget(containerRef.current.id, {
                onComplete: (data) => {
                    // Handle results
                }
            });
        }
    }, []);
    
    return <div id="paced-container" ref={containerRef}></div>;
}
```

### Option 4: CMS Integration
The widget works with any CMS that allows custom JavaScript:
- WordPress
- Drupal
- Joomla
- Webflow
- Squarespace (Business plan)
- Wix (Premium plan)

## Configuration Options

```javascript
new PACEDAssessmentWidget('container-id', {
    theme: 'default',           // Theme (currently only 'default')
    onComplete: function(data) {
        // Callback when assessment is completed
    },
    language: 'de',             // Language (currently only German)
    showResults: true,          // Show results page (default: true)
    allowRestart: true          // Allow restarting assessment (default: true)
});
```

## Data Structure

The widget returns assessment data in this format:

```javascript
{
    // Step 1 - Basic Information
    companySize: "250–999",
    industry: "Technologie & Software",
    teamSize: "6–10",
    teamMission: "User input text...",
    teamStructure: "User input text...",
    repetitiveWork: 45,
    
    // Step 2 - Strategic Priorities (1-5 scale)
    priorities: {
        mindset: 4,
        business_acumen: 5,
        employee_lifecycle: 3,
        // ... more fields
    },
    
    // Step 3 - Maturity Assessment (1-5 scale or 'unknown')
    maturity: {
        mindset: {
            0: 3,
            1: 4,
            2: 2
        },
        // ... more fields
    }
}
```

## Styling

The widget includes its own CSS styles and doesn't require external dependencies. All styles are prefixed with `paced-` to avoid conflicts.

To customize the appearance, you can override the CSS variables or specific classes:

```css
.paced-widget {
    --primary-color: #your-brand-color;
    --border-radius: 8px;
    /* ... other customizations */
}
```

## Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- IE 11 (with polyfills)

## File Size

- JavaScript: ~25KB (uncompressed)
- No external dependencies
- Self-contained CSS

## Security

- No external API calls during assessment
- Data is only sent when you implement the onComplete callback
- No cookies or local storage used by default
- XSS protection through proper DOM manipulation
