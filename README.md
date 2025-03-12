# CSS Animation Library

A lightweight, variable-based CSS animation system for creating smooth transitions with minimal code.

## Basic Usage

### Traditional Animations

Add the `.animate` class to any element you want to animate. Then add the `.active` class to trigger the animation.

```html
<div class="animate" style="--opacity-from: 0; --y-from: 20px;">
  This will fade in and move up
</div>

<script>
  // Trigger the animation
  document.querySelector('.animate').classList.add('active');
</script>
```

### Scroll-Driven Animations

Add the `.animate-timeline-scroll` class to create animations that progress based on scrolling:

```html
<div class="animate animate-timeline-scroll" style="
    --opacity-from: 0; 
    --y-from: 30px;
    --range-start: entry 10%; 
    --range-end: entry 50%;">
  This animates as you scroll
</div>
```

### View-Driven Animations

Add the `.animate-timeline-view` class to create animations that trigger when an element enters the viewport:

```html
<div class="animate animate-timeline-view" style="
    --opacity-from: 0; 
    --scale-from: 0.8;
    --range-start: entry; 
    --range-end: contain;">
  This animates when it comes into view
</div>
```

## Animation Variables

### Core Animation Controls

| Variable | Description | Default |
|----------|-------------|---------|
| `--props` | Properties to animate | `all` |
| `--duration` | Animation duration | `1s` |
| `--ease` | Timing function | `ease` |
| `--delay` | Animation delay | `0s` |

### Transform Properties

| Variable | Description | Default |
|----------|-------------|---------|
| `--x-from` | Initial horizontal position | `0` |
| `--x-to` | Final horizontal position | Same as `--x-from` |
| `--y-from` | Initial vertical position | `0` |
| `--y-to` | Final vertical position | Same as `--y-from` |
| `--z-from` | Initial depth position | `0` |
| `--z-to` | Final depth position | Same as `--z-from` |
| `--scale-from` | Initial scale | `1` |
| `--scale-to` | Final scale | Same as `--scale-from` |
| `--rotate-from` | Initial rotation | `0deg` |
| `--rotate-to` | Final rotation | Same as `--rotate-from` |

### Visual Properties

| Variable | Description | Default |
|----------|-------------|---------|
| `--opacity-from` | Initial opacity | `1` |
| `--opacity-to` | Final opacity | Same as `--opacity-from` |
| `--bg-from` | Initial background color | `initial` |
| `--bg-to` | Final background color | Same as `--bg-from` |
| `--color-from` | Initial text color | `initial` |
| `--color-to` | Final text color | Same as `--color-from` |
| `--width-from` | Initial width | `auto` |
| `--width-to` | Final width | Same as `--width-from` |
| `--height-from` | Initial height | `auto` |
| `--height-to` | Final height | Same as `--height-from` |
| `--filter-from` | Initial CSS filter | `initial` |
| `--filter-to` | Final CSS filter | Same as `--filter-from` |

### Timeline Animation Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `--range-start` | When animation starts | `normal` |
| `--range-end` | When animation ends | `normal` |

## Easing Presets

Add these classes to your element to use predefined easing functions:

| Class | Effect |
|-------|--------|
| `.ease-power1-out` | Gentle deceleration |
| `.ease-power2-out` | Moderate deceleration |
| `.ease-power3-out` | Strong deceleration |
| `.ease-power4-out` | Stronger deceleration |
| `.ease-back` | Slight overshoot |
| `.ease-elastic` | Springy overshoot |

## Examples

### Fade In From Bottom

```html
<div class="animate ease-power2-out" style="--opacity-from: 0; --y-from: 20px; --duration: 0.5s;">
  Content fades in from bottom
</div>
```

### Scale Up

```html
<div class="animate ease-back" style="--scale-from: 0.8; --opacity-from: 0; --duration: 0.7s;">
  Content scales up with slight bounce
</div>
```

### Scroll-Triggered Fade In

```html
<div class="animate animate-timeline-scroll" style="
    --opacity-from: 0; 
    --x-from: -30px;
    --range-start: entry; 
    --range-end: entry 60%;">
  This fades in and moves right as you scroll
</div>
```

### Enter Viewport Animation

```html
<div class="animate animate-timeline-view ease-back" style="
    --scale-from: 0.7; 
    --opacity-from: 0;
    --range-start: entry 10%; 
    --range-end: entry 60%;">
  This scales up with a bounce when it enters the viewport
</div>
```

### Rotate and Color Change

```html
<div class="animate ease-power3-out" style="--rotate-from: -45deg; --bg-from: #eee; --bg-to: #42A5F5; --duration: 1s;">
  Content rotates and changes color
</div>
```

### Filter Animation

```html
<div class="animate" style="--filter-from: grayscale(100%) blur(5px); --filter-to: grayscale(0%) blur(0px); --duration: 1.2s;">
  Image transitions from grayscale and blurry to colored and sharp
</div>
```

## Advanced Usage

### Staggered Animations

You can create staggered animations by setting different delays:

```html
<div class="animate ease-power2-out" style="--y-from: 30px; --opacity-from: 0; --delay: 0s;"></div>
<div class="animate ease-power2-out" style="--y-from: 30px; --opacity-from: 0; --delay: 0.1s;"></div>
<div class="animate ease-power2-out" style="--y-from: 30px; --opacity-from: 0; --delay: 0.2s;"></div>
```

### Animation Range Values

For scroll and view animations, you can use these range values:

- Percentages: `0%`, `50%`, `100%` (scroll position)
- Keywords: `entry` (element enters viewport), `contain` (element fully in viewport), `exit` (element leaves viewport)
- Combined: `entry 30%` (30% after element starts entering viewport)

```html
<!-- Animation runs from when element is 20% in view until fully in view -->
<div class="animate animate-timeline-view" style="
    --opacity-from: 0; 
    --range-start: entry 20%; 
    --range-end: contain;">
  Fades in as it enters view
</div>
```

### Reversing Animations

To reverse an animation, swap the values between the `--*-from` and `--*-to` variables:

```html
<!-- Going up -->
<div class="animate" style="--y-from: 0; --y-to: -20px;"></div>

<!-- Going down -->
<div class="animate" style="--y-from: -20px; --y-to: 0;"></div>
```

### Performance Tips

For smoother animations, especially on mobile:

1. Prefer transforming and opacity changes over other properties
2. Use `--props: transform, opacity` to limit transitions to those properties
3. For frequent animations, consider adding `will-change: transform, opacity` to your custom CSS
