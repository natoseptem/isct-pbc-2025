# 4.2 Variables & Assignment

## What You'll Learn

- What variables are and why we need them
- How to declare variables in JavaScript/TypeScript
- Different variable declaration keywords (`const`, `let`, `var`)
- How to display variable values on screen
- Using `console.log()` to inspect values

## What is a Variable?

A **variable** is a named container that stores a value.

### The Box Analogy

Think of a variable like a labeled box:

```
┌─────────────────┐
│  petName        │ ← Variable name (label)
├─────────────────┤
│  "Pochi"        │ ← Value (what's inside)
└─────────────────┘
```

You can:
- Put a value in the box (assignment)
- Look at what's in the box (read the value)
- Replace what's in the box (reassignment, in some cases)

### Why Use Variables?

**Without variables:**
```typescript
<h1>Pochi</h1>
<p>Pochi is 3 years old</p>
<p>Pochi is a Dog</p>
```

If you want to change "Pochi" to "Koro", you have to change it everywhere!

**With variables:**
```typescript
const petName = "Pochi"

<h1>{petName}</h1>
<p>{petName} is 3 years old</p>
<p>{petName} is a Dog</p>
```

Now you only change it in one place!

## Declaring Variables

### Syntax

```typescript
const variableName = value
```

- **`const`** - Keyword to declare a constant (can't be reassigned)
- **`variableName`** - The name you choose (camelCase convention)
- **`=`** - Assignment operator ("store this value")
- **`value`** - The data to store

### Examples

```typescript
const petName = "Pochi"
const petAge = 3
const petSpecies = "Dog"
const isVaccinated = true
```

## Variable Declaration Keywords

### `const` (Constant)

**Use for values that won't change:**

```typescript
const petName = "Pochi"
petName = "Koro" // ❌ Error! Can't reassign const
```

**This is the default choice** - use unless you need to reassign.

### `let` (Variable)

**Use when you need to reassign:**

```typescript
let petAge = 3
petAge = 4 // ✅ OK! Can reassign let
```

### `var` (Old-style Variable)

**Don't use this** - it's the old way with confusing scoping rules.

```typescript
var oldStyle = "don't use this" // ❌ Avoid
```

### When to Use Each

```typescript
// Use const by default
const petName = "Pochi"
const petSpecies = "Dog"

// Use let when you need to reassign
let petAge = 3
petAge = 4 // Age increases

// Never use var
```

## Exercise 1: Create Pet Variables

Let's store information about a pet.

### Task

Create variables for a pet's information.

### Steps

1. Open `app/page.tsx`

2. Add these variables inside the `Home` function, **before the `return` statement**:

```typescript
export default function Home() {
  // Pet information
  const petName = "Pochi"
  const petSpecies = "Dog"
  const petAge = 3
  const petColor = "Brown"

  console.log("Pet name:", petName)
  console.log("Pet species:", petSpecies)
  console.log("Pet age:", petAge)
  console.log("Pet color:", petColor)

  return (
    // ... existing JSX
  )
}
```

3. **Save** and check your browser console (F12 → Console)

You should see:
```
Pet name: Pochi
Pet species: Dog
Pet age: 3
Pet color: Brown
```

### What Happened?

- We declared 4 variables
- We logged their values to the console
- The console shows each value

## Displaying Variables in JSX

Now let's show these values on the page, not just in the console.

### Using Curly Braces `{}`

To insert a JavaScript expression in JSX, use `{}`:

```typescript
<h1>{petName}</h1>
// Displays: Pochi
```

The curly braces tell React: "This is JavaScript, not text!"

## Exercise 2: Display Pet Information

### Task

Display the pet variables on the page.

### Steps

1. Replace the JSX content with this:

```typescript
export default function Home() {
  // Pet information
  const petName = "Pochi"
  const petSpecies = "Dog"
  const petAge = 3
  const petColor = "Brown"

  return (
    <main className="flex min-h-screen flex-col items-center justify-center p-24 bg-gradient-to-b from-blue-50 to-white">
      <div className="text-center">
        <h1 className="text-4xl font-bold mb-8">🐾 Pet Management App 🐾</h1>

        <div className="bg-white rounded-lg shadow-lg p-8 max-w-md">
          <h2 className="text-2xl font-semibold mb-4">{petName}</h2>
          <p className="text-lg text-gray-700">Species: {petSpecies}</p>
          <p className="text-lg text-gray-700">Age: {petAge} years old</p>
          <p className="text-lg text-gray-700">Color: {petColor}</p>
        </div>
      </div>
    </main>
  )
}
```

2. **Save** and check the browser

You should see a card displaying Pochi's information!

### Understanding the Code

```typescript
<h2 className="text-2xl font-semibold mb-4">{petName}</h2>
```

- `{petName}` evaluates to the value of `petName`
- React inserts the value into the HTML
- The page shows: **Pochi**

### Try This

1. Change the values of the variables:

```typescript
const petName = "Whiskers"
const petSpecies = "Cat"
const petAge = 5
const petColor = "Orange"
```

2. **Save** - the page updates to show Whiskers!

3. Change back to Pochi or use your own pet's information

## JavaScript Expressions in JSX

You can put **any JavaScript expression** inside `{}`:

### Math Operations

```typescript
<p>Next year, {petName} will be {petAge + 1} years old</p>
```


### Conditional (Ternary) Operator

```typescript
<p>{petAge >= 10 ? "Senior" : "Young"}</p>
```



## Common Mistakes

### 1. Forgetting `const` or `let`

```typescript
// ❌ Wrong
petName = "Pochi" // Implicit global (bad!)

// ✅ Right
const petName = "Pochi"
```

### 2. Using Before Declaration

```typescript
// ❌ Wrong
console.log(petName)
const petName = "Pochi" // Error: can't use before declaration

// ✅ Right
const petName = "Pochi"
console.log(petName)
```

### 3. Reassigning `const`

```typescript
const petName = "Pochi"
petName = "Koro" // ❌ Error! Can't reassign const
```

Use `let` if you need to reassign:
```typescript
let petName = "Pochi"
petName = "Koro" // ✅ OK
```

### 4. Forgetting Curly Braces in JSX

```typescript
// ❌ Wrong
<h1>petName</h1>
// Displays literally: "petName"

// ✅ Right
<h1>{petName}</h1>
// Displays: "Pochi"
```

## TypeScript Type Annotations (Preview)

TypeScript lets you specify what type of value a variable should hold:

```typescript
const petName: string = "Pochi"
const petAge: number = 3
const isVaccinated: boolean = true
```

- **`string`** - Text values
- **`number`** - Numeric values (integers and decimals)
- **`boolean`** - `true` or `false`

**TypeScript infers types automatically**, so you usually don't need to write them:

```typescript
const petName = "Pochi" // TypeScript knows this is a string
```

We'll explore this more in the next section!

## Checkpoint

You should now be able to:

- ✅ Declare variables with `const` and `let`
- ✅ Display variable values in JSX using `{}`
- ✅ Perform calculations with variables


## What's Next?

Variables are great for single values, but what if you want to group related data together?

In the next section, you'll learn about **data structures** like objects and arrays to organize pet information better!

---

**Navigation:**
- **Previous:** [← 4.1 Hello World](01-hello-world.md)
- **Next:** [4.3 Data Structures →](03-data-structures.md)
- **Home:** [README](../../README.md)
