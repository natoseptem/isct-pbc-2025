# 4.5 Conditionals

## What You'll Learn

- If statements and else clauses
- Comparison and logical operators
- Ternary operator
- Conditional rendering in JSX
- Showing different content based on data

## What are Conditionals?

**Conditionals** let your code make decisions based on conditions.

### Real-World Example

```
IF it's raining
  THEN bring an umbrella
ELSE
  don't bring an umbrella
```

### In Code

```typescript
if (isRaining) {
  bringUmbrella()
} else {
  enjoyTheSun()
}
```

## Comparison Operators

Used to compare values:

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `===` | Equal to | `3 === 3` | `true` |
| `!==` | Not equal to | `3 !== 5` | `true` |
| `>` | Greater than | `5 > 3` | `true` |
| `<` | Less than | `3 < 5` | `true` |
| `>=` | Greater or equal | `5 >= 5` | `true` |
| `<=` | Less or equal | `3 <= 5` | `true` |

### Important: === vs ==

```typescript
3 === "3"   // false (strict equality, different types)
3 == "3"    // true (loose equality, converts types)
```

**Always use `===` and `!==`** (strict equality) - it's safer!

## Logical Operators

Combine multiple conditions:

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `&&` | AND (both must be true) | `true && true` | `true` |
| `\|\|` | OR (at least one true) | `true \|\| false` | `true` |
| `!` | NOT (inverts) | `!true` | `false` |

### Examples

```typescript
const age = 3
const species = "Dog"

// AND - both conditions must be true
if (age > 2 && species === "Dog") {
  console.log("Adult dog!")
}

// OR - at least one condition must be true
if (species === "Dog" || species === "Cat") {
  console.log("Common pet!")
}

// NOT - inverts the condition
if (!isVaccinated) {
  console.log("Needs vaccination!")
}
```

## If Statement

### Basic Syntax

```typescript
if (condition) {
  // Code runs if condition is true
}
```

### Example

```typescript
const age = 3

if (age < 2) {
  console.log("Puppy or kitten!")
}
```

## If-Else Statement

```typescript
if (condition) {
  // Runs if true
} else {
  // Runs if false
}
```

### Example

```typescript
const age = 3

if (age < 2) {
  console.log("Young")
} else {
  console.log("Not young")
}
```

## If-Else If-Else Chain

```typescript
if (condition1) {
  // Runs if condition1 is true
} else if (condition2) {
  // Runs if condition1 is false and condition2 is true
} else {
  // Runs if all conditions are false
}
```

### Example

```typescript
const age = 3

if (age < 2) {
  console.log("Baby")
} else if (age < 10) {
  console.log("Adult")
} else {
  console.log("Senior")
}
```

## Exercise 1: Add Age Category to PetCard

### Task

Show a badge indicating if the pet is young, adult, or senior.

### Steps

1. **Open** `components/PetCard.tsx`

2. **Add age category logic** inside the component, before the return:

```typescript
export default function PetCard({ name, species, age, color, breed }: PetCardProps) {
  // Emoji logic
  let emoji = "🐾"
  if (species === "Dog") emoji = "🐕"
  else if (species === "Cat") emoji = "🐱"
  else if (species === "Bird") emoji = "🐦"
  else if (species === "Fish") emoji = "🐠"

  // Determine age category
  let ageCategory = ""
  let ageCategoryColor = ""

  if (age < 2) {
    ageCategory = "Baby"
    ageCategoryColor = "bg-green-100 text-green-800"
  } else if (age < 8) {
    ageCategory = "Adult"
    ageCategoryColor = "bg-blue-100 text-blue-800"
  } else {
    ageCategory = "Senior"
    ageCategoryColor = "bg-purple-100 text-purple-800"
  }

  return (
    <div className="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow">
      <div className="flex items-center justify-between mb-4">
        <div className="flex items-center">
          <span className="text-4xl mr-3">{emoji}</span>
          <h2 className="text-2xl font-bold text-gray-800">{name}</h2>
        </div>
        <span className={`px-3 py-1 rounded-full text-sm font-semibold ${ageCategoryColor}`}>
          {ageCategory}
        </span>
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

3. **Save** and check the browser

You should see age badges on each pet card!

### Understanding the Code

```typescript
if (age < 2) {
  ageCategory = "Baby"
  ageCategoryColor = "bg-green-100 text-green-800"
}
```

- If age is less than 2, set category to "Baby" and green colors
- Otherwise, check the next condition

```typescript
<span className={`px-3 py-1 rounded-full text-sm font-semibold ${ageCategoryColor}`}>
  {ageCategory}
</span>
```

- Template literal allows inserting variable into className
- Display the age category text

## Exercise 2: Add Species-Specific Messages

### Task

Show a special message that changes based on the pet's species.

### Steps

1. **Open** `components/PetCard.tsx`

2. **Add after the info section:**

```typescript
<div className="mt-4 pt-4 border-t border-gray-200">
  <p className="text-sm text-gray-600 italic">
    {species === "Dog" ? "🦴 Loves playing fetch!" : null}
    {species === "Cat" ? "🐈 Enjoys napping in the sun!" : null}
    {species === "Bird" ? "🎵 Sings beautiful songs!" : null}
    {species === "Fish" ? "💧 Swims gracefully!" : null}
  </p>
</div>
```

3. Your full return should look like:

```typescript
return (
  <div className="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow">
    <div className="flex items-center justify-between mb-4">
      <div className="flex items-center">
        <span className="text-4xl mr-3">{emoji}</span>
        <h2 className="text-2xl font-bold text-gray-800">{name}</h2>
      </div>
      <span className={`px-3 py-1 rounded-full text-sm font-semibold ${ageCategoryColor}`}>
        {ageCategory}
      </span>
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

    <div className="mt-4 pt-4 border-t border-gray-200">
      <p className="text-sm text-gray-600 italic">
        {species === "Dog" ? "🦴 Loves playing fetch!" : null}
        {species === "Cat" ? "🐈 Enjoys napping in the sun!" : null}
        {species === "Bird" ? "🎵 Sings beautiful songs!" : null}
        {species === "Fish" ? "💧 Swims gracefully!" : null}
      </p>
    </div>
  </div>
)
```

4. **Save** and check the browser

Each species should show its special message!


## Switch Statement (Alternative to If-Else)

For multiple specific values:

```typescript
switch (species) {
  case "Dog":
    emoji = "🐕"
    break
  case "Cat":
    emoji = "🐱"
    break
  case "Bird":
    emoji = "🐦"
    break
  case "Fish":
    emoji = "🐠"
    break
  default:
    emoji = "🐾"
}
```

**When to use:**
- Many specific values to check
- Checking the same variable multiple times

**When not to use:**
- Complex conditions (use if-else)
- Range checks (use if-else)


## Common Mistakes

### 1. Using = Instead of ===

```typescript
// ❌ Wrong - assignment, not comparison!
if (age = 3) {
  // This assigns 3 to age, doesn't compare
}

// ✅ Right
if (age === 3) {
  // This compares age to 3
}
```

### 2. Forgetting Braces in If Statement

```typescript
// ⚠️ Only first line is conditional
if (age < 2)
  console.log("Young")
  console.log("Pet info") // Always runs!

// ✅ Use braces
if (age < 2) {
  console.log("Young")
  console.log("Pet info")
}
```

### 3. Confusing || and &&

```typescript
// AND (&&) - both must be true
if (age > 2 && species === "Dog") {
  // Adult AND dog
}

// OR (||) - at least one must be true
if (species === "Dog" || species === "Cat") {
  // Dog OR cat
}
```

## Checkpoint

You should now understand:

- ✅ If, else if, and else statements
- ✅ Comparison operators (===, !==, >, <, etc.)
- ✅ Logical operators (&&, ||, !)
- ✅ Conditional rendering in JSX

## What's Next?

You can now show/hide content based on conditions, but you're still manually creating three separate `<PetCard>` components.

In the next section, you'll learn about **loops** to automatically render a card for each pet in your array - no matter how many there are!

---

**Navigation:**
- **Previous:** [← 4.4 Displaying on Screen](04-displaying-on-screen.md)
- **Next:** [4.6 Loops →](06-loops.md)
- **Home:** [README](../../README.md)
