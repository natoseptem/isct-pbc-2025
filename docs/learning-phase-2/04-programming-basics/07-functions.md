# 4.7 Functions

## What You'll Learn

- What functions are and why they're useful
- Function syntax and parameters
- Return values
- Arrow functions
- Event handlers
- React state with useState

## What is a Function?

A **function** is a reusable block of code that performs a specific task.

### The Analogy

Think of a function like a recipe:

```
Recipe: Make Coffee
Inputs: coffee beans, water, milk, sugar
Steps:
  1. Grind coffee beans
  2. Brew with water
  3. Add milk and sugar
Output: A cup of coffee
```

In code:

```typescript
function makeCoffee(beans, water, milk, sugar) {
  // steps to make coffee
  return coffee
}
```

### Why Functions?

**Without functions:**
```typescript
// Repetitive code
const dog1Age = 3 * 7
const dog2Age = 5 * 7
const dog3Age = 2 * 7
```

**With functions:**
```typescript
function toDogYears(age) {
  return age * 7
}

const dog1Age = toDogYears(3)  // 21
const dog2Age = toDogYears(5)  // 35
const dog3Age = toDogYears(2)  // 14
```

**Benefits:**
- ✅ Reusable - write once, use many times
- ✅ Organized - code is easier to understand
- ✅ Maintainable - change logic in one place
- ✅ Testable - test functions independently

## Function Syntax

### Basic Syntax

```typescript
function functionName(parameter1, parameter2) {
  // code to execute
  return result
}
```

### Example

```typescript
function add(a, b) {
  return a + b
}

const sum = add(3, 5)  // 8
```

### Parts of a Function

1. **`function`** keyword
2. **Name** (camelCase)
3. **Parameters** in parentheses (inputs)
4. **Body** in curly braces (the code)
5. **`return`** statement (output)

## Parameters and Arguments

### Parameters

Variables listed in the function definition:

```typescript
function greet(name, age) {
  //         ↑     ↑
  //    parameters
}
```

### Arguments

Actual values passed when calling the function:

```typescript
greet("Pochi", 3)
//      ↑      ↑
//   arguments
```

### Example with Multiple Parameters

```typescript
function describePet(name, species, age) {
  return `${name} is a ${age} year old ${species}`
}

const result = describePet("Pochi", "Dog", 3)
console.log(result)  // "Pochi is a 3 year old Dog"
```

## Return Values

**`return`** sends a value back to the caller:

```typescript
function multiply(a, b) {
  return a * b
}

const result = multiply(4, 5)  // 20
console.log(result) // 20
```

### Function Without Return

```typescript
function logMessage(message) {
  console.log(message)
  // No return - returns undefined by default
}

const result = logMessage("Hello"
console.log(result) // undefined
```

### Multiple Return Statements

```typescript
function getAgeCategory(age) {
  if (age < 2) {
    return "Baby"
  } else if (age < 8) {
    return "Adult"
  } else {
    return "Senior"
  }
}

const result1 = getAgeCategory(1)
console.log(result1) // Baby
const result2 = getAgeCategory(2)
console.log(result2) // Adult
const result3 = getAgeCategory(8)
console.log(result3) // Senior
```

Once a `return` is executed, the function exits immediately.

## Exercise 1: Create Your First Function

### Task

Create a function that converts pet age to human years.

### Steps

1. **Create a new file:** `lib/petUtils.ts`

2. **Add the function:**

```typescript
/**
 * Convert pet age to human years
 * Dogs: age * 7
 * Cats: age * 5
 * Others: age * 3
 */
export function toHumanYears(age: number, species: string): number {
  if (species === "Dog") {
    return age * 7
  } else if (species === "Cat") {
    return age * 5
  } else {
    return age * 3
  }
}
```

**What's happening:**
- `export` makes this function available to other files
- Takes two parameters: `age` (number) and `species` (string)
- Returns a number (`: number` after parameters)
- Uses if-else to calculate based on species

### Using the Function in PetCard

1. **Open** `components/PetCard.tsx`

2. **Import the function at the top:**

```typescript
import { toHumanYears } from '../lib/petUtils'
```

3. **Use it in the component:**

Find the age display line and update it:

```typescript
<p className="text-gray-700">
  <span className="font-semibold">Age:</span> {age} years old ({toHumanYears(age, species)} in human years)
</p>
```

4. **Save** and check the browser - each pet should now show their age in human years!

**Example:** Pochi (3 years) → "3 years old (21 in human years)"

## Exercise 2: Add Age Category Function

### Task

Create a function that returns age category (Baby/Adult/Senior).

### Steps

1. **Open** `lib/petUtils.ts`

2. **Add the new function below `toHumanYears`:**

```typescript
/**
 * Get age category
 */
export function getAgeCategory(age: number): string {
  if (age < 2) {
    return "Baby"
  } else if (age < 8) {
    return "Adult"
  } else {
    return "Senior"
  }
}
```

**What's happening:**
- Takes one parameter: `age`
- Returns a string (`: string`)
- Uses multiple if-else to categorize age
- Function exits as soon as one return is executed

3. **Open** `components/PetCard.tsx`

4. **Update the import:**

```typescript
import { toHumanYears, getAgeCategory } from '../lib/petUtils'
```

5. **Use the function in the component:**

Add this near the top of the component function:

```typescript
export default function PetCard({ id, name, species, age, color, breed }: PetCardProps) {
  const ageCategory = getAgeCategory(age)
  const humanYears = toHumanYears(age, species)

  // ... rest of component
}
```

6. **Display the category:**

Add this after the name heading:

```typescript
<p className="text-sm text-gray-600">
  Category: {ageCategory}
</p>
```

7. **Save** and check - each pet should show their age category!

## Exercise 3: Add Species Emoji Function

### Task

Create a function that returns an emoji for each species.

### Steps

1. **Open** `lib/petUtils.ts`

2. **Add the function:**

```typescript
/**
 * Get emoji for species
 */
export function getSpeciesEmoji(species: string): string {
  switch (species) {
    case "Dog":
      return "🐕"
    case "Cat":
      return "🐱"
    case "Bird":
      return "🐦"
    case "Fish":
      return "🐠"
    default:
      return "🐾"
  }
}
```

**What's happening:**
- Uses `switch` statement to match species
- Each `case` handles one species
- `default` provides a fallback emoji

3. **Open** `components/PetCard.tsx`

4. **Update the import:**

```typescript
import { toHumanYears, getAgeCategory, getSpeciesEmoji } from '../lib/petUtils'
```

5. **Use it in the component:**

```typescript
export default function PetCard({ id, name, species, age, color, breed }: PetCardProps) {
  const emoji = getSpeciesEmoji(species)
  const ageCategory = getAgeCategory(age)
  const humanYears = toHumanYears(age, species)

  // ... rest of component
}
```

6. **Display the emoji before the name:**

```typescript
<h2 className="text-2xl font-bold text-gray-800">
  {emoji} #{id} {name}
</h2>
```

7. **Save** and check - each pet should have their species emoji!

## Function Best Practices

### 1. Name Functions Clearly

```typescript
// ❌ Vague
function doThing() { }

// ✅ Clear
function calculateTotalPrice() { }
function validateEmail() { }
function formatDate() { }
```

### 2. Keep Functions Small

Each function should do one thing well:

```typescript
// ❌ Too much responsibility
function processUserDataAndSendEmailAndLogActivity() { }

// ✅ Separate concerns
function processUserData() { }
function sendEmail() { }
function logActivity() { }
```

### 3. Use TypeScript Types

```typescript
// ❌ No types
function add(a, b) {
  return a + b
}

// ✅ With types
function add(a: number, b: number): number {
  return a + b
}
```

### 4. Provide Default Parameters

```typescript
function greet(name: string = "Guest") {
  return `Hello, ${name}!`
}

greet()           // "Hello, Guest!"
greet("Pochi")    // "Hello, Pochi!"
```

## Common Mistakes

### 1. Calling Function Instead of Passing It

```typescript
// ❌ Wrong - calls immediately
<button onClick={handleClick()}>Click</button>

// ✅ Right - passes function reference
<button onClick={handleClick}>Click</button>

// ✅ Also right - arrow function wrapper
<button onClick={() => handleClick()}>Click</button>
```

### 2. Forgetting Return

```typescript
// ❌ Wrong - no return
function add(a, b) {
  a + b  // This does nothing!
}

// ✅ Right
function add(a, b) {
  return a + b
}
```

### 3. Mutating State Directly

```typescript
// ❌ Wrong - mutates state
pets.push(newPet)
setPets(pets)  // React won't detect change!

// ✅ Right - create new array
setPets([...pets, newPet])
```

### 4. Using Wrong Arrow Function Syntax

```typescript
// ❌ Wrong - needs parentheses for object return
const getPet = () => { name: "Pochi" }  // Returns undefined!

// ✅ Right - wrap object in parentheses
const getPet = () => ({ name: "Pochi" })
```

## Checkpoint

You should now understand:

- ✅ Function syntax and structure
- ✅ Parameters and return values
- ✅ Creating reusable utility functions
- ✅ Importing and exporting functions
- ✅ Using functions in components

## What's Next?

You now know how to create functions, but you're writing a lot of code for common UI elements.

In the next section, you'll learn about **libraries** - specifically using recharts - to use pre-built, professional components and speed up development!

---

**Navigation:**
- **Previous:** [← 4.6 Loops](06-loops.md)
- **Next:** [4.8 Using Libraries →](08-libraries.md)
- **Home:** [README](../../README.md)
