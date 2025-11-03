# 4.4 Displaying on Screen

## What You'll Learn

- JSX syntax and rules
- What React components are
- How to create custom components
- Passing data with props
- Building a pet profile card component

## Understanding JSX

**JSX** (JavaScript XML) is a syntax extension that lets you write HTML-like code in JavaScript.

### JSX Rules

1. **Must return a single parent element:**

```typescript
// ❌ Wrong - multiple root elements
return (
  <h1>Title</h1>
  <p>Paragraph</p>
)

// ✅ Right - wrapped in parent
return (
  <div>
    <h1>Title</h1>
    <p>Paragraph</p>
  </div>
)

// ✅ Also right - React Fragment
return (
  <>
    <h1>Title</h1>
    <p>Paragraph</p>
  </>
)
```

2. **Close all tags:**

```typescript
// ❌ Wrong
<img src="/logo.png">
<input type="text">

// ✅ Right
<img src="/logo.png" />
<input type="text" />
```

3. **JavaScript expressions in `{}`:**

```typescript
<h1>{petName}</h1>
<p>Age: {age + 1}</p>
<div className={isActive ? "active" : "inactive"}></div>
```

## What are Components?

**Components** are reusable pieces of UI. Think of them as custom HTML tags.

### Why Components?

**Without components:**
```typescript
// Repeating the same code for each pet
<div className="card">
  <h2>Pochi</h2>
  <p>Dog</p>
</div>
<div className="card">
  <h2>Tama</h2>
  <p>Cat</p>
</div>
<div className="card">
  <h2>Piyo</h2>
  <p>Bird</p>
</div>
```

**With components:**
```typescript
<PetCard name="Pochi" species="Dog" />
<PetCard name="Tama" species="Cat" />
<PetCard name="Tweety" species="Bird" />
```

Much cleaner!

### Component Syntax

```typescript
function ComponentName() {
  return (
    <div>Content here</div>
  )
}
```

- Function name is PascalCase (capitalize first letter)
- Returns JSX
- Can be used as `<ComponentName />`

### Example: Simple Component

```typescript
function Greeting() {
  return <h1>Hello, World!</h1>
}

// Usage
<Greeting />
```

## Props: Passing Data to Components

**Props** (properties) are how you pass data to components.

### The Concept

```typescript
// Like HTML attributes
<img src="/photo.jpg" alt="A photo" />

// But for your custom components
<PetCard name="Pochi" species="Dog" age={3} />
```

### Receiving Props

```typescript
function PetCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>{props.species}</p>
      <p>{props.age} years old</p>
    </div>
  )
}
```

### Using Destructuring (Preferred)

```typescript
function PetCard({ name, species, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{species}</p>
      <p>{age} years old</p>
    </div>
  )
}
```

This "unpacks" the props object for easier access.

### TypeScript Props Type

```typescript
type PetCardProps = {
  name: string
  species: string
  age: number
}

function PetCard({ name, species, age }: PetCardProps) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{species}</p>
      <p>{age} years old</p>
    </div>
  )
}
```

## Exercise 1: Create a PetCard Component

### Task

Create a reusable component to display pet information.

### Steps

1. **Create a new file:** `components/PetCard.tsx`

In VSCode:
- Right-click the `components` folder
- Select "New File"
- Name it `PetCard.tsx`

2. **Write the component code:**

```typescript
type PetCardProps = {
  name: string
  species: string
  age: number
  color: string
  breed: string
}

export default function PetCard({ name, species, age, color, breed }: PetCardProps) {
  // Determine emoji based on species
  let emoji = "🐾"
  if (species === "Dog") emoji = "🐕"
  else if (species === "Cat") emoji = "🐱"
  else if (species === "Bird") emoji = "🐦"
  else if (species === "Fish") emoji = "🐠"

  return (
    <div className="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow">
      <div className="flex items-center mb-4">
        <span className="text-4xl mr-3">{emoji}</span>
        <h2 className="text-2xl font-bold text-gray-800">{name}</h2>
      </div>

      <div className="space-y-2">
        <p className="text-gray-700">
          <span className="font-semibold">Species:</span> {species}
        </p>
        <p className="text-gray-700">
          <span className="font-semibold">Age:</span> {age} years old
        </p>
        <p className="text-gray-700">
          <span className="font-semibold">Color:</span> {color}
        </p>
        <p className="text-gray-700">
          <span className="font-semibold">Breed:</span> {breed}
        </p>
      </div>
    </div>
  )
}
```

3. **Save** the file

### Understanding the Code

```typescript
export default function PetCard({ name, species, age, color, breed }: PetCardProps) {
```
- **`export default`** - Makes the component available for import
- **Destructuring** - Extracts props directly
- **Type annotation** - TypeScript knows what props to expect

```typescript
let emoji = "🐾"
if (species === "Dog") emoji = "🐕"
```
- Set emoji based on species
- We'll learn a better way to do conditionals soon!

## Exercise 2: Use the PetCard Component

### Task

Import and use the PetCard component in your page.

### Steps

1. **Open** `app/page.tsx`

2. **Import the component** at the top (below `'use client';` ):

```typescript
import PetCard from '../components/PetCard'
```

3. **Use the component** in your JSX:

```typescript
type Pet = {
  name: string
  species: string
  age: number
  color: string
  breed: string
}

export default function Home() {
  const pets: Pet[] = [
    {
      name: "Pochi",
      species: "Dog",
      age: 3,
      color: "Brown",
      breed: "Golden Retriever"
    },
    {
      name: "Tama",
      species: "Cat",
      age: 5,
      color: "Orange",
      breed: "Persian"
    },
    {
      name: "Tweety",
      species: "Bird",
      age: 2,
      color: "Yellow",
      breed: "Canary"
    }
  ]

  return (
    <main className="min-h-screen bg-gradient-to-b from-blue-50 to-white p-8">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-12">
          <h1 className="text-5xl font-bold text-gray-900 mb-4">
            🐾 Pet Management App 🐾
          </h1>
          <p className="text-xl text-gray-600">
            Managing {pets.length} wonderful pets
          </p>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <PetCard
            name={pets[0].name}
            species={pets[0].species}
            age={pets[0].age}
            color={pets[0].color}
            breed={pets[0].breed}
          />
          <PetCard
            name={pets[1].name}
            species={pets[1].species}
            age={pets[1].age}
            color={pets[1].color}
            breed={pets[1].breed}
          />
          <PetCard
            name={pets[2].name}
            species={pets[2].species}
            age={pets[2].age}
            color={pets[2].color}
            breed={pets[2].breed}
          />
        </div>
      </div>
    </main>
  )
}
```

4. **Save** and check the browser!

You should see 3 beautiful pet cards in a grid!

## Common Mistakes

### 1. Forgetting to Import

```typescript
// ❌ Error: PetCard is not defined
<PetCard {...pet} />

// ✅ Add import at top
import PetCard from '../components/PetCard'
```

### 2. Wrong File Path

```typescript
// ❌ Wrong
import PetCard from './PetCard'  // Not in same folder

// ✅ Right
import PetCard from '../components/PetCard'  // Up one level, then into components
```

### 3. Forgetting Export

```typescript
// ❌ No export in PetCard.tsx
function PetCard() { ... }

// ✅ Add export
export default function PetCard() { ... }
```

### 4. Wrong Prop Types

```typescript
// ❌ Passing string where number expected
<PetCard age="3" />  // TypeScript error!

// ✅ Pass number
<PetCard age={3} />
```

### 5. Using class instead of className

```typescript
// ❌ Wrong
<div class="container">

// ✅ Right
<div className="container">
```

## Checkpoint

You should now understand:

- ✅ JSX syntax and rules
- ✅ Creating functional components
- ✅ Passing props to components
- ✅ TypeScript prop types

## What's Next?

You can now create components and pass props, but you're manually creating three `<PetCard>` components.

What if you have 100 pets? You need **conditionals** (to show/hide elements) and **loops** (to render multiple items automatically).

In the next sections, you'll learn these essential programming concepts!

---

**Navigation:**
- **Previous:** [← 4.3 Data Structures](03-data-structures.md)
- **Next:** [4.5 Conditionals →](05-conditionals.md)
- **Home:** [README](../../README.md)
