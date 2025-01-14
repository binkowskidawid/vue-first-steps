# Vue First Steps: Job Board Vue.js Project 🚀

Welcome to the Vue Jobs Board project! This isn't just another tutorial - we're building a real-world job board
application that helps connect Vue.js developers with exciting opportunities. And hey, React developer, guess what?
You're about to join the Vue.js community not just as a learner, but as a job board creator! So you've decided to
venture into the Vue.js world? Don't worry, we've got your back! Think of this as learning a new dialect of the same
language - you already know how to build awesome UIs, now you're just learning a different way to express it.

## Project Attribution

This project builds upon the foundation provided by Brad Traversy's Vue Crash Course
2024 (https://github.com/bradtraversy/vue-crash-2024). We've expanded the original code base with TypeScript integration
and additional features while maintaining the core job board functionality. We encourage you to check out Brad's
original course for an excellent introduction to Vue.js fundamentals. So you've decided to venture into the Vue.js
world? Don't worry, we've got your back! Think of this as learning a new dialect of the same language - you already know
how to build awesome UIs, now you're just learning a different way to express it.

## Table of Contents

- [Introduction](#introduction)
- [Component Setup: Options API vs Composition API](#component-setup-options-api-vs-composition-api)
- [State Management: The Vue Way](#state-management-the-vue-way)
- [Template Syntax: JSX's Fancy Cousin](#template-syntax-jsxs-fancy-cousin)
- [Event Handling: Goodbye onClick, Hello @click](#event-handling-goodbye-onclick-hello-click)
- [Lifecycle Methods: The Circle of Vue](#lifecycle-methods-the-circle-of-vue)

## Introduction

Remember when you first learned React and everyone was like "JSX is weird"? Well, welcome to Vue templates - they're
like JSX's cousin who went to art school. They're more structured but equally expressive!

## Component Setup: Options API vs Composition API

Vue gives you two ways to write components: Options API (the classic way) and Composition API (the React-like way).
Let's look at both:

### Options API (Traditional Vue)

```vue

<script lang="ts">
  export default {
    data(): {
      name: string;
      status: 'active' | 'inactive' | 'loading';
    } {
      return {
        name: 'John Doe',
        status: 'active'
      }
    },
    methods: {
      changeStatus() {
        // Methods use 'this' to access component's data
        if (this.status === 'active') {
          this.status = 'loading'
        }
      }
    }
  }
</script>
```

Think of Options API as your organized friend who keeps everything in labeled boxes. Data goes in `data()`, methods go
in `methods`, computed properties in `computed`, etc.

### Composition API (The React Dev's Comfort Zone)

```vue

<script setup lang="ts">
  import { ref } from 'vue'

  // Look familiar? It's like useState!
  const name = ref('John Doe')
  const status = ref<'active' | 'inactive' | 'loading'>('active')

  function changeStatus() {
    // No more 'this'! Just use .value
    if (status.value === 'active') {
      status.value = 'loading'
    }
  }
</script>
```

Hey React dev, feeling more at home? The Composition API is like React hooks' sibling. Instead of `useState`, you use
`ref` or `reactive`. The main difference? You need to use `.value` to access/modify ref values (think of it as Vue's
version of array destructuring from useState).

## State Management: The Vue Way

React:

```jsx
const [tasks, setTasks] = useState(['eat', 'sleep', 'code'])

const addTask = (newTask) => {
  setTasks([...tasks, newTask])
}
```

Vue (Composition API):

```vue
const tasks = ref(['eat', 'sleep', 'code'])

function addTask(newTask) {
tasks.value.push(newTask) // Direct mutation is fine in Vue!
}
```

Plot twist: Vue actually likes mutations! No need for immutable updates - Vue's reactivity system handles it all for
you.

## Template Syntax: JSX's Fancy Cousin

React's JSX:

```jsx
{
  status === 'active' ? (
    <p>Online</p>
  ) : status === 'inactive' ? (
    <p>Offline</p>
  ) : (
    <p>Loading</p>
  )
}

{
  tasks.map((task, index) => (
    <li key={task}>{task}</li>
  ))
}
```

Vue's Template:

```vue
<p v-if="status === 'active'">Online</p>
<p v-else-if="status === 'inactive'">Offline</p>
<p v-else>Loading</p>

<li v-for="(task, index) in tasks" :key="task">
  {{ task }}
</li>
```

Vue templates are like JSX with built-in directives. Instead of using ternary operators and map functions, you get nice,
readable directives like `v-if` and `v-for`.

## Event Handling: Goodbye onClick, Hello @click

React:

```jsx
<button onClick={handleClick}>Click me</button>
<form onSubmit={(e) => {
  e.preventDefault()
  handleSubmit()
}}>
```

Vue:

```vue

<button @click="handleClick">Click me</button>
<form @submit.prevent="handleSubmit">
```

Vue's event handling is like React's but with some syntactic sugar. The `@` symbol is shorthand for `v-on:`, and
`.prevent` is like calling `e.preventDefault()`. Neat, right?

## Lifecycle Methods: The Circle of Vue

React:

```jsx
useEffect(() => {
  // Component mounted
  fetchData()

  return () => {
    // Cleanup
  }
}, [])
```

Vue:

```vue
onMounted(async () => {
// Component mounted
await fetchData()
})

onUnmounted(() => {
// Cleanup
})
```

The concepts are the same, just with different names. `useEffect` with empty deps array = `onMounted`, cleanup
function = `onUnmounted`.

## Pro Tips for React Developers

1. Don't fight the framework! Vue has opinions about how things should be done, and that's okay.
2. Embrace the template syntax - it might feel weird at first, but it's actually quite powerful.
3. Start with the Composition API if you're coming from React - it'll feel more natural.
4. Remember that `.value` is your friend when using `ref` - it's like the Vue tax we all have to pay.
5. Take advantage of Vue's reactivity system - no need for immutable updates!

## Common "Gotchas" for React Developers

1. Forgetting `.value` when working with refs (We've all been there!)
2. Trying to use JSX syntax in templates (`className` instead of `class`, anyone?)
3. Fighting the reactivity system with unnecessary spreads and immutable updates
4. Looking for `useEffect` instead of `onMounted` (Old habits die hard!)

Remember: Vue is not React with different syntax - it's its own framework with its own patterns and best practices.
Embrace the differences, and you might find yourself loving some of Vue's unique features!

## About This Project

### What We're Building 🏗️

We're creating a Vue.js job board platform where companies can post Vue.js-related positions and developers can find
their dream Vue jobs. Think of it as a specialized job marketplace just for the Vue community!

### Technical Stack 🛠️

```json
{
  "Frontend Framework": "Vue.js 3.5.13",
  "Build Tool": "Vite 6.0.5",
  "Styling": "Tailwind CSS 3.4.17",
  "Type Safety": "TypeScript 5.6.3",
  "Code Quality": {
    "Linting": "ESLint 9.14.0",
    "Formatting": "Prettier 3.3.3"
  }
}
```

### Project Features ✨

1. **Job Listings Display**: A responsive grid of job posts using Tailwind CSS for beautiful, responsive layouts
2. **Filtering System**: Smart filtering options for job type, location, and experience level
3. **Job Posting Form**: A form for employers to submit new job listings
4. **Type Safety**: Full TypeScript integration for a robust development experience

### Getting Started 🚀

1. Clone the repository:
   ```bash
   git clone https://github.com/binkowskidawid/vue-first-steps.git
   cd vue-first-steps
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Available scripts:
   ```bash
   npm run dev        # Start development server
   npm run build      # Build for production
   npm run type-check # Run TypeScript checks
   npm run lint       # Lint your code
   npm run format     # Format with Prettier
   ```

### Project Structure 📁

```
vue-first-steps/
├── src/
│   ├── components/   # Reusable Vue components
│   ├── router/       # Vue router configuration
│   ├── views/        # View components
│   ├── types/        # TypeScript type definitions
│   └── assets/       # Static assets
├── public/           # Public static files
├── _theme_files/     # Theme files
├── index.html        # HTML template
└── package.json      # Project dependencies and scripts
```

### Development Tips 💡

1. Use Vite's hot module replacement (HMR) during development - it's blazing fast!
2. Leverage Vue DevTools for debugging - they're already configured in the project
3. Take advantage of Tailwind's utility classes for rapid UI development
4. TypeScript and ESLint will help catch errors before they reach production

### Contributing 🤝

Feel free to contribute to this project! Whether it's:

- Adding new features
- Fixing bugs
- Improving documentation
- Suggesting enhancements

All contributions are welcome!

Happy coding! 🎉

P.S. If you find yourself typing `useState` instead of `ref`, don't worry - we've all been there. The muscle memory will
catch up eventually! 😄

P.P.S. And remember, every great Vue developer started somewhere - maybe even with a React background just like you! 💪
