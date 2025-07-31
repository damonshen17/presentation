## The "Traditional" Way

<p>Let's start with one button and see how the code grows...</p>
<div class="layout-box">
  <pre><code class="css" data-line-numbers="1-5|6-8|9-11">
/* Red Button */
.btn-red { 
  background-color: #e53e3e; 
  color: white; 
}
.btn-red:hover { 
  background-color: #c53030; 
}

/* Blue Button */
.btn-blue { 
  background-color: #3182ce; 
  color: white; 
}
.btn-blue:hover { 
  background-color: #2b6cb0; 
}

/* Green Button */
.btn-green { 
  background-color: #38a169; 
  color: white; 
}
.btn-green:hover { 
  background-color: #2f855a; 
}
  </code></pre>
  <div class="button-column">
    <button class="btn red fragment" data-fragment-index="0">Red Button</button>
    <button class="btn blue fragment" data-fragment-index="1">Blue Button</button>
    <button class="btn green fragment" data-fragment-index="2">Green Button</button>
  </div>
</div>

---

## A "Smarter" Way: CSS Filters

<p>We can refactor to a generic `.btn` class with a hover `filter`...</p>
<div class="layout-box">
  <pre><code class="css" data-line-numbers="1-6|7|8|9">
.btn {
  color: white;
  transition: filter 0.2s;
}
.btn:hover {
  filter: brightness(85%);
}
.btn-red { 
  background-color: #e53e3e; 
}
.btn-blue { 
  background-color: #3182ce; 
}
.btn-green { 
  background-color: #38a169; 
}
  </code></pre>
  <div class="button-column">
    <button class="btn red filter fragment" data-fragment-index="0">Red Button</button>
    <button class="btn blue filter fragment" data-fragment-index="1">Blue Button</button>
    <button class="btn green filter fragment" data-fragment-index="2">Green Button</button>
  </div>
</div>

---

## The Modern Way: `color-mix()`

<p>Using `color-mix()` gives us the most power and control...</p>
<div class="layout-box">
  <pre><code class="css" data-line-numbers="1-6|7|8|9">
.btn {
  background-color: var(--base-color);
  color: white;
  transition: background-color 0.2s;
}
.btn:hover {
  background-color: color-mix(in oklch, var(--base-color), black 20%);
}
.btn-red { 
  --base-color: oklch(63% 0.26 29); 
}
.btn-blue { 
  --base-color: oklch(60% 0.18 264); 
}
.btn-green { 
  --base-color: oklch(65% 0.19 150); 
}
  </code></pre>
  <div class="button-column">
    <button class="btn mix-red fragment" data-fragment-index="0">Red Button</button>
    <button class="btn mix-blue fragment" data-fragment-index="1">Blue Button</button>
    <button class="btn mix-green fragment" data-fragment-index="2">Green Button</button>
  </div>
</div>

---

## Q&A

---

## Why `color-mix()` Works Now: Additive vs Subtractive Color

<div class="color-theory-layout">
  <div class="fragment" data-fragment-index="0">
    <h3>🖥️ Additive (RGB)</h3>
    <p>Light-based mixing: Red + Green + Blue = White</p>
    <div class="additive-demo">
      <div class="rgb-circles">
        <div class="circle red-light"></div>
        <div class="circle green-light"></div>
        <div class="circle blue-light"></div>
      </div>
    </div>
  </div>
  
  <div class="fragment" data-fragment-index="1">
    <h3>🎨 Subtractive (Paint/Ink)</h3>
    <p>Pigment-based mixing: Colors absorb light, get darker</p>
    <div class="subtractive-demo">
      <div class="paint-mix">
        <span>Blue + Yellow = Green</span>
        <span>Red + Blue = Purple</span>
      </div>
    </div>
  </div>
</div>

<div class="fragment" data-fragment-index="2">
  <h3>🎯 OKLCH Enables True Subtractive Mixing</h3>
  <ul>
    <li class="fragment" data-fragment-index="3"><strong>Perceptual uniformity:</strong> Colors mix as humans expect them to</li>
    <li class="fragment" data-fragment-index="4"><strong>No unwanted hue shifts:</strong> Blue + White = Light Blue (not purple!)</li>
    <li class="fragment" data-fragment-index="5"><strong>Natural darkening:</strong> Adding black creates realistic shadows</li>
    <li class="fragment" data-fragment-index="6"><strong>Consistent results:</strong> Same mixing ratios produce predictable outcomes</li>
  </ul>
</div>