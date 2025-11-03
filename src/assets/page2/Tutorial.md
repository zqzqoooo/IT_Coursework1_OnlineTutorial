# Complete Vue.js Tutorial: Build a "Highland Games Event Planner" from Scratch

**Tutorial Goal:** Welcome to this complete guide to Vue.js! This tutorial will take you from zero, installing all necessary tools in a clean Ubuntu environment, configuring and creating a Vue.js project, learning its core modules, and finally building a fully functional web app (complete with add, delete, and persistence features).

## Part 1: Environment Setup (Ubuntu & Node.js)

In preparing to write any code, you need a reliable development environment. This tutorial will use **WSL (Windows Subsystem for Linux)** to run a full Ubuntu system on Windows.

> **Note:** If you are on macOS or a desktop Linux (like Ubuntu Desktop), your system is already set. You just need to skip to **Step 3** of this section and install Node.js.

### Step 1: Install WSL 2 and Ubuntu on Windows

1.  **Open PowerShell as Administrator**:
    * Click the Start Menu, search for "PowerShell".
    * Right-click "Windows PowerShell" and select "Run as administrator".

2.  **Install WSL**:
    * In PowerShell, enter the following command and press Enter:
        ```powershell
        wsl --install
        ```
    * This command automatically enables the required Windows features, downloads the latest Linux kernel, and installs the **Ubuntu** distribution by default.
    * After the installation is complete, **restart your computer**.
    
    ![alt text](/IT_Coursework1_OnlineTutorial/src/assets/page2/images/md-1.png)

3.  **Initialize Ubuntu**:
    * After restarting, Ubuntu will launch automatically. If not, you can find it in your Start Menu.
    * On the first launch, it will ask you to create a new **UNIX username and password**.
    * **Important:** This password is used when you need to install software (using `sudo`) in this Ubuntu environment. Remember it.

### Step 2: (Best Practice) Install Node.js using nvm

We don't recommend installing Node.js directly. Instead, we'll use **nvm** (Node Version Manager). This allows you to easily switch between different Node.js versions for different projects.

1.  **Open your Ubuntu terminal**.

2.  **Update package lists**:
    ```bash
    sudo apt update
    ```

3.  **Install `curl`** (used to download the nvm install script):
    ```bash
    sudo apt install curl
    ```

4.  **Install nvm**:
    ```bash
    curl -o- [https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh](https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh) | bash
    ```

5.  **Activate nvm** (close and reopen your terminal, or run):
    ```bash
    source ~/.bashrc
    ```

6.  **Install the Node.js LTS version**:
    * LTS (Long Term Support) is the most stable version.
        ```bash
        nvm install --lts
        ```

7.  **Verify installation**:
    ```bash
    node -v
    npm -v
    ```
    If you see version numbers (e.g., `v20.11.1` and `10.2.4`), congratulations, your environment is ready!
    
    ![alt text](/IT_Coursework1_OnlineTutorial/src/assets/page2/images/md-2.png)

---

## Part 2: Project Configuration (Creating the Vue Project)

Now you will use the officially recommended tool, `Vite` (an extremely fast build tool), to create your Vue project.

1.  In your Ubuntu terminal, navigate to a directory where you like to keep your projects (e.g., `~/projects`), and run:
    ```bash
    npm create vue@latest
    ```

2.  You will see an interactive menu.

    ```bash
    ┌  Vue.js - The Progressive JavaScript Framework
    │
    ◇  Project name (target directory):
    │  vue-highland-games
    ```
    * **Project name:** Type your project name, like `vue-highland-games`, and press **Enter**.

3.  Next is the **"Select features"** menu.

    ```bash
    ◇  Select features to include in your project: (↑/↓ to navigate, space to select, a to toggle all, enter to confirm)
    │  none
    ```
    * **How to use:**
        * Use the **Up/Down arrow keys (↑/↓)** to move the cursor.
        * Use the **Spacebar** to select or deselect a feature.
        * Once you've made your selections, press **Enter** to confirm.

    * **Our Selections:**
        We only need two features: **ESLint** and **Prettier**. Use the arrow keys and spacebar to select them.
        * `❯ ◉ TypeScript`
        * `  ◯ JSX Support`
        * `  ◯ Vue Router for Single-Page Application development?`
        * `  ◯ Pinia for state management?`
        * `  ◯ Vitest for Unit Testing?`
        * `  ◉ ESLint for code quality?`
        * `  ◉ Prettier for code formatting?`

    * **Why these choices?**
        * **TypeScript (No):** Adds strict type-checking to JS. It's great for large projects but adds complexity to our tutorial.
        * **JSX Support (No):** JSX is a syntax for writing HTML in JavaScript (used by React). Vue uses HTML-like templates by default, which are more beginner-friendly.
        * **Vue Router (No):** Used for managing "pages" (e.g., `/home`, `/about`). Our app is a single page.
        * **Pinia (No):** A state management library. Useful for large apps where many components need to share data.
        * **Vitest (No):** Used for "unit testing," which is outside the scope of this tutorial.
        * **ESLint (Yes):** **(Recommended)** A "linter" that checks your code for errors as you type, saving you from common bugs.
        * **Prettier (Yes):** **(Recommended)** A "code formatter" that automatically standardizes your code style (like indentation and semicolons).

    * After selecting **ESLint** and **Prettier**, press **Enter** to confirm.

4.  **"Select experimental features"**
    ```bash
    ◇  Select experimental features to include in your project: (↑/↓ to navigate, space to select, a to toggle all, enter to
    confirm)
    │  none
    ```
    * **Selection:** We don't need any experimental features. Just press **Enter** to skip (keeping `none`).

5.  **"Skip all example code"**
    ```bash
    ◇  Skip all example code and start with a blank Vue project?
    │  No
    ```
    * **Selection:** **No** (Press **Enter** to select the default "No").
    * **Explanation:** We want it to generate the example `App.vue` file so we have a base to modify.

6.  **Done!**
    * The tool will scaffold your project and display:
    ```bash
    Scaffolding project in /home/heshanws/vue-highland-games...
    │
    └  Done. Now run:

      cd vue-highland-games
      npm install
      npm run dev
    ```

7.  **Start the project**:
    * Follow the instructions in your terminal to enter the project and start it:
        ```bash
        cd vue-highland-games
        npm install     # Installs all dependencies
        npm run dev     # Starts the development server
        ```

8.  In your **Windows browser**, open the address it shows (usually `http://localhost:5173/`). You will see the Vue welcome page!
![alt text](/IT_Coursework1_OnlineTutorial/src/assets/page2/images/md-3.png)
---

## Part 3: Introduction to Core Modules (Composition API)

Before building, you must understand Vue's core concepts.

#### 1. Single File Component (SFC)
A Vue project is made of `.vue` files. Each file is a component, containing three parts:
* `<template>`: Holds the HTML structure.
* `<script setup>`: Holds the JavaScript logic (**All our code will go here**).
* `<style scoped>`: Holds the CSS styles (`scoped` means the styles only apply to this component).

#### 2. Reactivity (`ref`)
This is Vue's "magic".
* **Function:** `ref` converts a normal JS variable (like a string, number, or array) into a "reactive reference".
* **Usage:** When you change the value of this reference, Vue automatically updates every part of the `<template>` that uses it.
* **Note:** In `<script>`, you **must** use `.value` to access or modify its value.
* **Example:**
    ```javascript
    import { ref } from 'vue'
    const message = ref('Hello')
    console.log(message.value) // "Hello"
    message.value = 'Goodbye'  // This will trigger an update
    ```

#### 3. Template Syntax
* **Interpolation (`{{ }}`)**: `<h1>{{ message }}</h1>`. Used to display a `ref`'s value in the HTML.
* **Attribute Binding (`:`)**: Short for `v-bind`. Used to dynamically bind HTML attributes.
    ```html
    <div class="my-class"></div>
    <div :class="myClassName"></div>
    ```
* **Event Listening (`@`)**: Short for `v-on`. Used to listen for DOM events (like a click).
    ```html
    <button @click="myFunction">Click Me</button>
    ```

#### 4. Common Directives
* **`v-model` (Two-Way Binding)**: The perfect partner for `ref`. It "binds" a form input to a `ref` variable in both directions.
    ```html
    <input v-model="message">
    ```
    (Now, the input's content and `message.value` will always be in sync.)

* **`v-if` / `v-else` (Conditional Rendering)**:
    ```html
    <p v-if="events.length > 0">You still have events.</p>
    <p v-else>No events left.</p>
    ```

* **`v-for` (List Rendering)**:
    ```html
    <ul>
      <li v-for="event in events" :key="event.id">
        {{ event.name }}
      </li>
    </ul>
    ```
    ( **`key` is required.** It helps Vue efficiently track each item.)

#### 5. Component Communication
* **`defineProps`**: How a child component **receives** data from its parent.
* **`defineEmits`**: How a child component **sends a message** (emits an event) to its parent (e.g., "Please delete me!").

#### 6. Lifecycle (`onMounted`)
`onMounted` is a "lifecycle hook" that runs automatically **after** the component has been rendered to the page. It's the perfect time to **fetch initial data** from a server or local storage.

#### 7. Watcher (`watch`)
`watch` is used to "watch" a `ref`. As soon as that `ref`'s value changes, the `watch` function will run. It's the perfect time to **save data**.

---

## Part 4: Building the Project (The Event Planner)

Now, let's combine all these modules!

**Goal:** Build an app that can add, delete, and **persist** events (data won't be lost on refresh).

### Step 1: `App.vue` (The Parent Component)

Open `src/App.vue` and replace **all** of its content with the following code. This is your "main" component.

```html
<script setup>
// Modules: Import all needed functions
// ref: For creating reactive data
// onMounted: To run code after component loads (for loading data)
// watch: To watch for data changes (for saving data)
import { ref, onMounted, watch } from 'vue'

// Modules: Import the child component
// We need EventItem to display each item in our list
import EventItem from './components/EventItem.vue'

// --- State Definition ---

// newEventName will store the text from the input box
const newEventName = ref('')
// events will store our entire list of event objects
const events = ref([]) // Start with an empty array
// Define a key for localStorage
const STORAGE_KEY = 'vue-highland-events'

// --- Data Persistence ---

// Modules: Lifecycle (onMounted)
// 1. This function runs automatically when the component loads
onMounted(() => {
  // Try to read previously saved data from localStorage
  const savedEvents = localStorage.getItem(STORAGE_KEY)
  // If data was found...
  if (savedEvents) {
    // ...fill our events list with it
    // JSON.parse converts the string back into an array object
    events.value = JSON.parse(savedEvents)
  }
})

// Modules: Watcher (watch)
// 2. Watch the 'events' array. As soon as it changes, save it.
watch(events, (newEventList) => {
  // JSON.stringify converts the array object into a string for storage
  localStorage.setItem(STORAGE_KEY, JSON.stringify(newEventList))
}, { 
  // 'deep: true' is essential. It tells watch to look inside
  // the array for changes (like adding/removing an object)
  deep: true 
})

// --- Core Logic (Functions) ---

// 3. Function to add a new event
function addEvent() {
  // Prevent adding empty or whitespace-only names
  if (newEventName.value.trim() === '') {
    return
  }
  
  // Add a new object to the events array
  events.value.push({
    id: Date.now(), // Use a timestamp as a unique ID
    name: newEventName.value
  })
  
  // Clear the input box for the next entry
  newEventName.value = ''
}

// 4. Function to handle the delete request from a child
//    This function will receive the eventId from the child
function handleDelete(eventId) {
  // Use .filter() to create a new array without the deleted item
  // This is an immutable operation. Vue detects that
  // events.value is assigned a new array and updates the view.
  events.value = events.value.filter(event => event.id !== eventId)
}
</script>

<template>
  <main>
    <h1>Highland Games Event Planner</h1>
    
    <form @submit.prevent="addEvent">
      <input 
        v-model="newEventName" 
        placeholder="Enter a new event...">
      <button type="submit">Add Event</button>
    </form>
    
    <h2>Event List</h2>
    
    <ul v-if="events.length > 0">
      
      <EventItem 
        v-for="event in events" 
        :key="event.id"
        :event="event"
        @delete-event="handleDelete"
      />
      </ul>
    
    <p v-else>
      All clear! Add your first event.
    </p>

  </main>
</template>

<style>
/* Global styles (no 'scoped' attribute)
   These apply to the whole app, including child components
*/
body { 
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; 
  background: #f4f4f4; 
}

main { 
  max-width: 600px; 
  margin: 40px auto; 
  padding: 20px 40px; 
  background: #fff; 
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

h1 {
  color: #42b883; /* Vue Green */
  text-align: center;
}

h2 {
  color: #333;
  border-bottom: 2px solid #f4f4f4;
  padding-bottom: 10px;
}

form {
  display: flex;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #eee;
  border-radius: 4px;
}

button {
  background: #42b883; 
  color: white; 
  border: none;
  padding: 10px 15px;
  margin-left: 10px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background: #36a473;
}

ul {
  list-style: none;
  padding: 0;
}

p {
  text-align: center;
  color: #888;
}
</style>
```

### Step 2: `EventItem.vue` (The Child Component)

1.  Create a new folder named `components` inside your `src` folder.
2.  Inside `src/components/`, create a new file named `EventItem.vue`.
3.  Paste the following **complete** code. This component's only job is to display the event and request deletion.

<!-- end list -->

```html
<script setup>
// Modules: Props and Emits
// 1. Declare that it receives an 'event' object from its parent (App.vue)
const props = defineProps({
  event: {
    type: Object,
    required: true
  }
})

// 2. Declare that this component will emit a 'delete-event' event
//    defineEmits is also a macro
const emit = defineEmits(['delete-event'])

// 3. This function is called when the delete button is clicked
function requestDelete() {
  // 4. CRITICAL: Emit the 'delete-event' and pass the ID
  //    (props.event.id is now accessible thanks to our 'props' constant)
  //    App.vue is listening for this and will receive the ID
  emit('delete-event', props.event.id)
}
</script>

<template>
  <li class="event-item">
    <span class="event-name">{{ event.name }}</span>
    
    <button @click="requestDelete" class="delete-btn">Delete</button>
  </li>
</template>

<style scoped>
/* 'scoped' means these styles ONLY apply to this component,
   and won't leak out to App.vue or other components.
*/
.event-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background: #fff;
  border: 1px solid #eee;
  border-radius: 4px;
  margin-bottom: 10px;
}

.event-name {
  color: #333;
}

.delete-btn {
  background-color: #ff4d4d;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  padding: 5px 10px;
  font-size: 0.9em;
}

.delete-btn:hover {
  background-color: #e60000;
}
</style>
```
![alt text](/IT_Coursework1_OnlineTutorial/src/assets/page2/images/md-4.png)
-----

## Part 5: Final Code Dissection

You've built the app. Now, let's understand exactly *why* it works.

### 1\. `App.vue` (The Parent Component / State Manager)

`App.vue` acts as the "brain" of your project. It manages all the data (state) and core logic.

**`App.vue` `<script setup>` Dissection:**

  * `import { ref, onMounted, watch }`
      * `ref`: Creates all reactive data (`newEventName`, `events`).
      * `onMounted`: **Loads Data**. A lifecycle hook that runs **once** when the component first loads. We use it to read from `localStorage`, enabling persistence.
      * `watch`: **Saves Data**. A listener that "watches" the `events` array. As soon as `events` changes (add or delete), the `watch` function runs, saving the new array to `localStorage`. `{ deep: true }` is essential for it to watch *inside* the array.
  * `const events = ref([])`
      * This is the **"Single Source of Truth"** for the application. All events are stored here.
  * `function addEvent() { ... }`
      * This function **mutates** the `events` array by `.push()`ing a new object with a unique ID (`Date.now()`).
  * `function handleDelete(eventId) { ... }`
      * This function also **mutates** the `events` array. It uses `.filter()`—a modern, immutable JS practice. It doesn't modify the original array but returns a **new** array *without* the deleted item. Vue detects that `events.value` was assigned a new array and updates the view.

**`App.vue` `<template>` Dissection:**

  * `<form @submit.prevent="addEvent">`
      * `@submit.prevent`: This is beautiful Vue syntax. `@submit` listens for the form submission (like pressing Enter). `.prevent` is a **modifier** that automatically calls `event.preventDefault()`, stopping the page from reloading.
  * `<EventItem ... />` (The most critical interaction)
      * `v-for="event in events" :key="event.id"`: Loops through the `events` array, creating one `EventItem` component instance for each object. `:key` is required for performance.
      * `:event="event"`: **"Props Down"**. The parent `App.vue` **passes** the individual `event` object *down* to the child `EventItem` via a prop named `event`.
      * `@delete-event="handleDelete"`: **"Events Up"**. The parent `App.vue` **listens** for a **custom event** named `delete-event` emitted by the child. When it "hears" this event, it calls its own `handleDelete` function.

### 2\. `EventItem.vue` (The Child Component / Presentational Component)

`EventItem.vue` is a "dumb" component (or "presentational component"). It doesn't manage any state. Its only jobs are:

1.  Display the data it's given (via `props`).
2.  Tell the parent when something needs to happen (via `emit`).

**`EventItem.vue` `<script setup>` Dissection:**

  * `const props = defineProps({ event: Object })`
      * **\!\! Critical Fix \!\!** `defineProps` is a macro that **returns** an object containing all declared props. We **must** assign this to a `props` constant. This is how we access the data inside our `<script>` logic (e.g., in the `requestDelete` function) using `props.event`.
  * `const emit = defineEmits(['delete-event'])`
      * This line declares all **events** this component is allowed to emit. It tells Vue, "I might emit a 'delete-event' at some point."
  * `function requestDelete() { ... }`
      * A local function called when the user clicks the "Delete" button.
      * `emit('delete-event', props.event.id)`: This is the "Event Up" in action. It **emits** the event we declared, and attaches a **payload** (`props.event.id`). This payload is passed directly to the parent's listener function (i.e., `App.vue`'s `handleDelete(eventId)`).

### Data Flow Summary:

1.  **Data Flow:** `App.vue` -\> `events` array -\> `v-for` -\> `:event` prop -\> `EventItem.vue` (Data flows **down**).
2.  **Event Flow:** `EventItem.vue` (User Click) -\> `requestDelete()` -\> `emit('delete-event', id)` -\> `App.vue` (`@delete-event="handleDelete"`) -\> `handleDelete(id)` function (Events flow **up**).

-----

**Tutorial Complete\!**

You have successfully built a complete Vue.js application from scratch. You've learned not only how to set up your environment and write code, but more importantly, you've understood Vue's core **component-based, reactive system** and the fundamental design pattern of **"Props Down, Events Up"**.