# ⚛️ React Fundamentals — Module 01

> *From zero to first render — everything you need to know*

---

## 01 · What is React?

**React is an external library** — a bundle of code that *someone else wrote*, which you load into your project so you don't have to build everything from scratch.

> 💡 **External Library** = code that lives *outside* your own files. You reference it and get all of its power for free.

```
React (External Library) → Loaded into your file → Build websites much easier ✓
```

---

## 02 · Why Two Libraries?

You load **both** `react` AND `react-dom` — but why aren't they the same thing?

| Library | Purpose | Platforms |
|---|---|---|
| `react` | The **core engine** — shared logic, virtual DOM, components | 🌐 Web + 📱 Mobile |
| `react-dom` | The **web-specific bridge** — talks to the browser's real DOM | 🌐 Web only |

### Platform Flowcharts

```
react  +  react-dom     →  🌐 Web App (Website)
react  +  react-native  →  📱 Mobile App (iOS / Android)
```

> 🎯 **Key insight:** `react` is shared across all platforms. Only the *renderer* changes — `react-dom` for web, `react-native` for mobile.

---

## 03 · Minimum React Setup

The **absolute minimum** code to get React running in a browser:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My React App</title>
    <!-- Load React core -->
    <script src="https://unpkg.com/react/umd/react.development.js"></script>
    <!-- Load ReactDOM (web renderer) -->
    <script src="https://unpkg.com/react-dom/umd/react-dom.development.js"></script>
  </head>
  <body>
    <!-- React mounts into this div -->
    <div id="js"></div>

    <script>
      // Step 1: grab the container element
      const container = document.querySelector('#js');

      // Step 2: create a React root, Step 3: render into it
      ReactDOM.createRoot(container).render("WELCOME");
    </script>
  </body>
</html>
```

### Breaking Down `ReactDOM.createRoot(container).render(...)`

```
ReactDOM  →  .createRoot(container)       →  .render("WELCOME")  →  🖥️ "WELCOME" appears
              Sets up React inside the div    Displays it on screen
```

| Part | What It Does |
|---|---|
| `document.querySelector('#js')` | Finds the `<div id="js">` — this is where React will live |
| `ReactDOM.createRoot(container)` | **Sets up React** inside that div. Builds the stage. |
| `.render("WELCOME")` | **Displays something** on that stage — text, HTML, components |

---

## 04 · JSX vs JavaScript

> **JSX = HTML inside JavaScript**

JSX lets you write what *looks like* HTML directly in your `.js` file. Under the hood, it compiles to regular JS automatically.

### Side-by-Side Comparison

**✨ JSX Way (easier)**
```jsx
// Write HTML-like syntax directly
const button = <button>HELLO</button>;
```

**📜 Plain JS Way (harder)**
```js
// Must do everything manually
const button = document.createElement('button');
button.innerHTML = 'HELLO';
```

> ✅ Both do the **exact same thing**. JSX is just a nicer way to write it.

| Myth | Reality |
|---|---|
| "JSX is real HTML" | ❌ It only *looks* like HTML |
| "JSX is a separate language" | ❌ It compiles down to plain JavaScript |
| "You must use JSX" | ❌ It's optional, but highly recommended |

---

## 05 · The Render Rule

> ⚠️ **Critical rule:** `.render()` can only accept **ONE** top-level element. You cannot pass it two or three separate elements!

### ❌ WRONG — Two separate elements

```jsx
const button = <button>Click me</button>;
const para   = <p>Hello</p>;

// ❌ This FAILS — render only takes ONE value
ReactDOM.createRoot(container).render(button, para);
```

### ✅ CORRECT — Wrapped in a `<div>`

```jsx
// Wrap multiple elements in ONE container div
const content = (
  <div>
    <button>Click me</button>
    <p>Hello</p>
  </div>
);

// ✅ Works — ONE root element passed in
ReactDOM.createRoot(container).render(content);
```

### Why `<div>` Fixes It

```
button ❌           Wrap in         div ✓              🖥️ Both elements
para   ❌    →    <div> container  →  (1 root element)  →  appear on screen
(2 roots)          (acts as a box)    render is happy!
```

> 📦 **What is a `<div>`?**
> A `<div>` is a **container** — invisible on screen, but wraps multiple elements together as children of ONE parent. That satisfies render's "one element only" requirement.

---

## 06 · Full Working Example

Putting it all together — multiple elements, JSX, div wrapper:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First React App</title>
    <script src="react.development.js"></script>
    <script src="react-dom.development.js"></script>
    <script src="babel.min.js"></script>  <!-- converts JSX → JS -->
  </head>
  <body>
    <div id="js"></div>

    <script type="text/babel">
      const container = document.querySelector('#js');

      // div wraps everything so render receives ONE element
      const content = (
        <div>
          <h1>Welcome to React!</h1>
          <button>Click Me</button>
          <p>Hello, world!</p>
        </div>
      );

      ReactDOM.createRoot(container).render(content);
    </script>
  </body>
</html>
```

> 📌 **Note on Babel:** Babel converts JSX syntax into regular JS that the browser understands. Without it, the browser won't know what `<button>` inside JS means. In real projects (Vite, Create React App), this is handled automatically.

---

## 07 · Quick Reference Cheatsheet

| Concept | What To Remember | Example |
|---|---|---|
| `react` | External library. Load it in. | `<script src="react.js">` |
| `react-dom` | Web-specific renderer. Puts things on screen. | `<script src="react-dom.js">` |
| `createRoot` | Sets up React inside a container div. | `ReactDOM.createRoot(div)` |
| `render` | Displays **ONE** element on screen. | `.render(<div>...</div>)` |
| JSX | HTML-like syntax inside JS. Easier to write. | `const btn = <button>Hi</button>` |
| `<div>` wrapper | Wrap multiple elements so render sees only one. | `<div> ...all elements... </div>` |

---

*⚛️ React Fundamentals · Module 01*
