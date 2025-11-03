# 4.6 Loops

## What You'll Learn

- Why loops are essential
- Array `map()` method
- Rendering lists in React
- The importance of keys
- Filtering arrays

## Why Loops?

Currently, you're rendering pet cards like this:

```typescript
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
```

**Problems:**
- Manual and repetitive
- Hard to maintain
- Doesn't scale (what if you have 100 pets?)
- Need to update code when adding/removing pets

**Solution:** Use loops to automatically generate components!

## The map() Method

The `map()` method loops through an array and creates something for each element.
In React, we use `map()` to loop through data and create JSX elements.

### Basic Syntax

```typescript
array.map((element) => {
  return <JSX using element data>
})
```

**Think of it as:**
- "For each item in the array..."
- "...create a component using that item's data"

## Using map() in JSX

You can use `map()` to generate JSX elements:

```typescript
const pets = ["Pochi", "Tama", "Piyo"]

return (
  <div>
    {pets.map((pet) => (
      <h2>{pet}</h2>
    ))}
  </div>
)
```

**Result:**
```html
<div>
  <h2>Pochi</h2>
  <h2>Tama</h2>
  <h2>Piyo</h2>
</div>
```

## Exercise 1: Render All Pets with map()

### Task

Replace the manual pet cards with a loop.

### Steps

1. **Open** `app/page.tsx`

2. **Replace the manual cards** with a map:

```typescript
export default function Home() {
  const pets: Pet[] = [
    {
      name: "Pochi",
      species: "Dog",
      age: 3,
      color: "Brown",
      breed: "Golden Retriever",
    },
    {
      name: "Tama",
      species: "Cat",
      age: 5,
      color: "Orange",
      breed: "Persian",
    },
    {
      name: "Piyo",
      species: "Bird",
      age: 2,
      color: "Yellow",
      breed: "Canary",
    },
    {
      name: "Masuo",
      species: "Fish",
      age: 1,
      color: "Blue",
      breed: "Betta",
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
          {pets.map((pet) => (
            <PetCard key={pet.name} {...pet} />
          ))}
        </div>
      </div>
    </main>
  )
}
```

3. **Save** and check the browser

You should see all 4 pets rendered automatically!

### Try Adding More Pets

Add a 5th pet to the array:

```typescript
{
  name: "Koro",
  species: "Dog",
  age: 7,
  color: "Black",
  breed: "Labrador",
  isVaccinated: true
}
```

Save - the new pet appears automatically! No need to add another `<PetCard>` manually.

### Understanding the Code

```typescript
{pets.map((pet) => (
  <PetCard key={pet.name} {...pet} />
))}
```

**Breaking it down:**
- `pets.map()` - Iterate over the pets array
- `(pet) =>` - Arrow function, `pet` is each element
- `<PetCard ... />` - Return a PetCard for each pet
- `{...pet}` - Spread all pet properties as props
- `key={pet.name}` - Unique identifier (explained below)

## The key Prop

When rendering lists, React needs a unique `key` for each element.

### Why Keys?

React uses keys to:
- Track which items changed
- Update efficiently
- Preserve component state
- Improve performance

### Key Requirements

1. **Must be unique** among siblings
2. **Should be stable** (don't change between renders)
3. **Should not use array index** if list order can change

### Good Keys

```typescript
// Using unique ID (best)
{pets.map((pet) => (
  <PetCard key={pet.id} {...pet} />
))}

// Using unique name (OK if names are unique)
{pets.map((pet) => (
  <PetCard key={pet.name} {...pet} />
))}
```

### What Happens Without Keys?

React will show a warning in the console:

```
Warning: Each child in a list should have a unique "key" prop.
```

**Always add keys when using map()!**

## Exercise 2: Add Unique IDs

### Task

Add unique IDs to pets for better keys.

### Steps

1. **Update the Pet type:**

```typescript
type Pet = {
  id: number  // Add this
  name: string
  species: string
  age: number
  color: string
  breed: string
}
```

2. **Add IDs to each pet:**

```typescript
const pets: Pet[] = [
  {
    id: 1,
    name: "Pochi",
    species: "Dog",
    age: 3,
    color: "Brown",
    breed: "Golden Retriever"
  },
  {
    id: 2,
    name: "Tama",
    species: "Cat",
    age: 5,
    color: "Orange",
    breed: "Persian"
  },
  {
    id: 3,
    name: "Piyo",
    species: "Bird",
    age: 2,
    color: "Yellow",
    breed: "Canary"
  },
  {
    id: 4,
    name: "Masuo",
    species: "Fish",
    age: 1,
    color: "Blue",
    breed: "Betta"
  }
]
```

3. **Use ID in key:**

```typescript
{pets.map((pet) => (
  <PetCard key={pet.id} {...pet} />
))}
```

4. **Update PetCard to accept and display id:**

In `components/PetCard.tsx`:

```typescript
type PetCardProps = {
  id: number  // Add this
  name: string
  species: string
  age: number
  color: string
  breed: string
  isVaccinated: boolean
}

export default function PetCard({ id, name, species, age, color, breed}: PetCardProps) {
  // ... existing code ...

  return (
    <div className="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow">
      <h2 className="text-2xl font-bold text-gray-800 mb-4">
        #{id} {name}  {/* Display ID before name */}
      </h2>
      {/* ... rest of the card content ... */}
    </div>
  )
}
```

5. **Save** and check the browser - each pet card should now show its ID number before the name (like "#1 Pochi")!

## Filtering Arrays

Often you want to show only some items from an array.

### The filter() Method

The `filter()` method creates a new array with only elements that pass a test:

```typescript
const dogs = pets.filter((pet) => pet.species === "Dog")
// Returns array containing only dogs
```

**How it works:**
1. Goes through each pet
2. Checks if `pet.species === "Dog"` is true
3. If true, includes it in the new array
4. If false, skips it

### Chaining filter() and map()

You can chain `filter()` and `map()` together:

```typescript
{pets
  .filter((pet) => pet.species === "Dog")  // First, keep only dogs
  .map((pet) => (                          // Then, create cards
    <PetCard key={pet.id} {...pet} />
  ))
}
```

## Exercise 3: Filter Pets by Species

### Task

Show only dogs by adding a filter to your code.

### Steps

1. **Open** `app/page.tsx`

2. **Find the section where you map pets:**

```typescript
{pets.map((pet) => (
  <PetCard key={pet.id} {...pet} />
))}
```

3. **Add a filter before the map:**

```typescript
{pets
  .filter((pet) => pet.species === "Dog")
  .map((pet) => (
    <PetCard key={pet.id} {...pet} />
  ))}
```

4. **Save** and check - you should only see #1 Pochi!

### Try Different Filters

**Show only cats:**
```typescript
.filter((pet) => pet.species === "Cat")
```
Result: Only #2 Tama

**Show only birds:**
```typescript
.filter((pet) => pet.species === "Bird")
```
Result: Only #3 Piyo

**Show only fish:**
```typescript
.filter((pet) => pet.species === "Fish")
```
Result: Only #4 Masuo

**Show all pets again:**
Remove the `.filter()` line:
```typescript
{pets.map((pet) => (
  <PetCard key={pet.id} {...pet} />
))}
```

## Other Array Methods

### find()

Returns the first element that matches:

```typescript
const pochi = pets.find((pet) => pet.name === "Pochi")
console.log(pochi) // { name: "Pochi", ... }
```

### some()

Returns true if ANY element matches:

```typescript
const hasUnvaccinated = pets.some((pet) => !pet.isVaccinated)
console.log(hasUnvaccinated) // true or false
```

### every()

Returns true if ALL elements match:

```typescript
const allVaccinated = pets.every((pet) => pet.isVaccinated)
console.log(allVaccinated) // true or false
```

### reduce()

Accumulates values:

```typescript
const totalAge = pets.reduce((sum, pet) => sum + pet.age, 0)
console.log(totalAge) // Sum of all ages
```

## Common Mistakes

### 1. Forgetting to Return

```typescript
// ❌ Wrong - no return
{pets.map((pet) => {
  <PetCard {...pet} />
})}

// ✅ Right - implicit return with ()
{pets.map((pet) => (
  <PetCard {...pet} />
))}

// ✅ Also right - explicit return
{pets.map((pet) => {
  return <PetCard {...pet} />
})}
```

### 2. Missing Key

```typescript
// ❌ Wrong - no key
{pets.map((pet) => (
  <PetCard {...pet} />
))}

// ✅ Right - has key
{pets.map((pet) => (
  <PetCard key={pet.id} {...pet} />
))}
```
## Checkpoint

You should now understand:

- ✅ Why loops are essential
- ✅ Using `map()` to transform arrays
- ✅ Rendering lists in JSX
- ✅ The importance of unique keys
- ✅ Filtering arrays with `filter()`
- ✅ Chaining array methods

## What's Next?

You can now render dynamic lists.

In the next section, you'll learn about **functions** - how to create reusable logic and handle user interactions!

---

**Navigation:**
- **Previous:** [← 4.5 Conditionals](05-conditionals.md)
- **Next:** [4.7 Functions →](07-functions.md)
- **Home:** [README](../../README.md)
