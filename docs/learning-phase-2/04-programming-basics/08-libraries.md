# 4.8 Using Libraries

## What You'll Learn

- What libraries are and why they're useful
- Installing packages with npm
- Using recharts for data visualization
- Creating pie charts and bar charts
- Understanding library components

## What are Libraries?

**Libraries** (also called packages) are pre-written code that you can use in your projects.

### The Analogy

Building software is like building a house:

**Without libraries:**
```
Make bricks from scratch
Cut wood from trees
Mine iron for nails
Mix concrete
↓
Build the house (years of work)
```

**With libraries:**
```
Buy bricks, wood, nails, concrete
↓
Build the house (months or weeks of work)
```

Libraries let you focus on what makes your app unique, not reinventing common solutions!

### Example: Creating a Graph

**Without a library:**
- Write 500+ lines of code
- Handle complex SVG drawing
- Implement tooltips, legends, animations
- Test on different browsers
- Fix bugs for edge cases
- Time: 1-2 weeks

**With recharts library:**
- Write 10-20 lines of code
- Use pre-built components
- Everything works out of the box
- Time: 10-15 minutes

### Common Types of Libraries

1. **UI Components** - Pre-built visual elements
   - shadcn/ui, Material-UI, Chakra UI

2. **Data Visualization** - Charts and graphs
   - recharts, Chart.js, D3.js

3. **Date/Time** - Working with dates
   - date-fns, Moment.js, Day.js

4. **Forms** - Handling form validation
   - React Hook Form, Formik

5. **Utilities** - Helper functions
   - lodash, clsx

## Why Use Libraries?

### 1. Save Time and Focus on Your App

Spend time on features that make your app unique, not common problems.

```typescript
// Without library: 500 lines of SVG code
// With recharts:
<PieChart width={400} height={300}>
  <Pie data={data} dataKey="value" />
</PieChart>
```

### Other Benefits

1. **Documentation** - Clear guides and examples
2. **Community Support** - Ask questions, get help
3. **Updates** - Bug fixes and new features
4. **Reliability** - Used in production by many companies
5. **Best Practices** - Follow standards

## What is recharts?

**recharts** is a charting library built for React.

### Key Features

- **Easy to use** - Works like React components
- **Declarative** - Write JSX to create charts
- **TypeScript support** - Great type safety
- **Responsive** - Charts adapt to screen size
- **Customizable** - Change colors, sizes, styles

### Chart Types

- Pie Chart (円グラフ)
- Bar Chart (棒グラフ)
- Line Chart (折れ線グラフ)
- Area Chart (面グラフ)
- And more!

## Exercise 1: Install recharts

### Task

Add the recharts library to your project.

### Steps

1. **Stop your dev server** (if running)

Press `Ctrl+C` in the terminal where `npm run dev` is running.

2. **Install recharts:**

```bash
npm install recharts
```

You should see output like:
```
added 1 package, and audited X packages in Xs
```

3. **Verify installation:**

Open `package.json` and look for recharts in dependencies:

```json
"dependencies": {
  "recharts": "^3.3.0",
  // ... other packages
}
```

4. **Restart the dev server:**

```bash
npm run dev
```

**What just happened?**
- npm downloaded recharts from the npm registry
- Added it to your `node_modules` folder
- Recorded it in `package.json`
- Now you can import and use recharts components!

## Exercise 2: Create a Pie Chart

### Task

Create a pie chart showing the distribution of pet species.

### Steps

1. **Create a new component:** `components/PetSpeciesChart.tsx`

2. **Add the code:**

```typescript
import { PieChart, Pie, Cell, Tooltip, Legend } from 'recharts'

type Pet = {
  id: number
  name: string
  species: string
  age: number
  color: string
  breed: string
}

type PetSpeciesChartProps = {
  pets: Pet[]
}

export default function PetSpeciesChart({ pets }: PetSpeciesChartProps) {
  // Count pets by species
  const dogCount = pets.filter(p => p.species === "Dog").length
  const catCount = pets.filter(p => p.species === "Cat").length
  const otherCount = pets.filter(p => p.species !== "Dog" && p.species !== "Cat").length

  // Prepare data for the chart
  const data = [
    { id: 1, name: 'Dogs', value: dogCount },
    { id: 2, name: 'Cats', value: catCount },
    { id: 3, name: 'Others', value: otherCount }
  ]

  const COLORS = ['#FF6B6B', '#4ECDC4', '#FFE66D']

  return (
    <div className="bg-white rounded-lg shadow-lg p-6">
      <h2 className="text-2xl font-bold mb-4 text-center">Pet Species Distribution</h2>
      <PieChart width={400} height={300}>
        <Pie
          data={data}
          cx={200}
          cy={150}
          labelLine={false}
          label
          outerRadius={80}
          fill="#8884d8"
          dataKey="value"
        >
          {data.map((entry) => (
            <Cell key={entry.id} fill={COLORS.find((_, i) => i === entry.id - 1)} />
          ))}
        </Pie>
        <Tooltip />
        <Legend />
      </PieChart>
    </div>
  )
}
```

**What's happening:**
- Takes `pets` array as a prop - more flexible and reusable!
- Counts Dogs and Cats separately, everything else goes to "Others"
- Each data object has an `id` - used as a unique key when mapping
- `data.map((entry) =>` - Loop through data using the `id` as key
- `key={entry.id}` - React needs unique keys for list items
- `PieChart` - Container for the entire chart
- `Pie` - The actual pie chart
- `Cell` - Used to color each slice differently
- `Tooltip` - Shows details when you hover
- `Legend` - Shows what each color means

3. **Open** `app/page.tsx`

4. **Import the component:**

Add at the top:
```typescript
import PetSpeciesChart from '../components/PetSpeciesChart'
```

5. **Add the chart to your page:**

Inside the return, before the pet cards grid:

```typescript
return (
  <main className="min-h-screen bg-gradient-to-b from-blue-50 to-white p-8">
    <div className="max-w-6xl mx-auto">
      <h1 className="text-5xl font-bold text-center mb-8 text-gray-900">
        🐾 Pet Management Dashboard 🐾
      </h1>

      {/* Add the chart here */}
      <div className="mb-8 flex justify-center">
        <PetSpeciesChart pets={pets} />
      </div>

      {/* Pet cards grid */}
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {pets.map((pet) => (
          <PetCard key={pet.id} {...pet} />
        ))}
      </div>
    </div>
  </main>
)
```

**Much simpler!** Just pass the entire `pets` array - the component handles the counting.

6. **Save** and check the browser

You should see a colorful pie chart showing the distribution of your pets!

**Try hovering over the chart** - you'll see tooltips with details!

## Exercise 3: Create a Bar Chart

### Task

Create a bar chart showing the age distribution of pets.

### Steps

1. **Create a new component:** `components/PetAgeChart.tsx`

2. **Add the code:**

```typescript
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend } from 'recharts'
import { getAgeCategory } from '../lib/petUtils'

type Pet = {
  id: number
  name: string
  species: string
  age: number
  color: string
  breed: string
}

type PetAgeChartProps = {
  pets: Pet[]
}

export default function PetAgeChart({ pets }: PetAgeChartProps) {
  // Count pets by age category
  const babyCount = pets.filter(p => getAgeCategory(p.age) === "Baby").length
  const adultCount = pets.filter(p => getAgeCategory(p.age) === "Adult").length
  const seniorCount = pets.filter(p => getAgeCategory(p.age) === "Senior").length

  // Prepare data for the chart
  const data = [
    { id: 1, category: 'Baby (0-1)', count: babyCount },
    { id: 2, category: 'Adult (2-7)', count: adultCount },
    { id: 3, category: 'Senior (8+)', count: seniorCount }
  ]

  return (
    <div className="bg-white rounded-lg shadow-lg p-6">
      <h2 className="text-2xl font-bold mb-4 text-center">Age Distribution</h2>
      <BarChart width={500} height={300} data={data}>
        <CartesianGrid strokeDasharray="3 3" />
        <XAxis dataKey="category" />
        <YAxis />
        <Tooltip />
        <Legend />
        <Bar dataKey="count" fill="#8884d8" />
      </BarChart>
    </div>
  )
}
```

**What's happening:**
- Takes `pets` array as a prop - reusable component!
- Imports `getAgeCategory` function from utilities
- Uses `filter()` and `getAgeCategory()` to count each age group
- Each data object has an `id` - used for unique identification
- `BarChart` - Container for bar chart
- `CartesianGrid` - Background grid lines
- `XAxis` / `YAxis` - The axes of the chart
- `Bar` - The actual bars showing data
- `dataKey="category"` - Use "category" field for X-axis labels
- `dataKey="count"` - Use "count" field for bar heights

3. **Open** `app/page.tsx`

4. **Import the component:**

```typescript
import PetAgeChart from '../components/PetAgeChart'
```

5. **Add the bar chart below the pie chart:**

```typescript
<div className="mb-8 flex justify-center">
  <PetSpeciesChart pets={pets} />
</div>

{/* Add age chart */}
<div className="mb-8 flex justify-center">
  <PetAgeChart pets={pets} />
</div>
```

**Super simple!** Just pass the `pets` array to both charts.

6. **Save** and check - you now have two charts showing different insights!

## Evaluating and Choosing Libraries

### Where to Evaluate Libraries

1. **Package Registry**
   - Search for packages
   - See download stats
   - Read documentation
   - ex) https://www.npmjs.com/ (npm Regisry)

2. **GitHub** - See source code, issues and documents

### How to Evaluate a Library

**Check these factors:**

1. **Downloads per week** - Popular = well-tested
   - recharts: 2M+ downloads/week ✅

2. **Last update** - Recently maintained?
   - recharts: Updated regularly ✅

3. **GitHub stars** - Community approval
   - recharts: 20K+ stars ✅

4. **Documentation** - Easy to understand?
   - recharts: Excellent docs ✅

5. **TypeScript support** - Type definitions included?
   - recharts: Full TypeScript support ✅

6. **License** - Can you legally use it?
   - **MIT License** - ✅ Free to use, modify, and distribute (most common)
   - **Apache 2.0** - ✅ Free to use, includes patent protection
   - **GPL** - ⚠️ Requires your code to be open source too
   - **Proprietary** - ❌ May require payment or have restrictions
   - recharts: MIT License ✅

7. **Bundle size** - Will it slow down your app?
   - recharts: Reasonable size ✅

### Understanding Open Source Licenses

**MIT License (Most Common):**
- ✅ Use in commercial projects
- ✅ Modify the code
- ✅ Distribute copies
- ✅ No need to open source your code
- Example: React, Next.js, recharts

**Apache 2.0:**
- Similar to MIT
- Additional patent protection
- Example: TypeScript

**GPL (General Public License):**
- ⚠️ If you use it, your entire project must be open source
- Not suitable for commercial closed-source projects

**Where to find the license:**
- Check `package.json` → `"license": "MIT"`
- Look for `LICENSE` file in GitHub repository
- npm package page shows the license

## Common npm Commands

```bash
# Install a package
npm install package-name

# Install a specific version
npm install package-name@1.2.3

# Uninstall a package
npm uninstall package-name

# Update packages
npm update

# List installed packages
npm list

# Check for outdated packages
npm outdated
```

## Checkpoint

You should now understand:

- ✅ What libraries are and why they're useful
- ✅ How to install libraries with npm
- ✅ How to import and use library components
- ✅ How to create charts with recharts
- ✅ How to evaluate libraries before using them

## What's Next?

You can now use external libraries to add powerful features quickly!

In the next section, you'll learn about **Team Development** - using Git and GitHub to collaborate with others, create branches, and handle merge conflicts!

---

**Navigation:**
- **Previous:** [← 4.7 Functions](07-functions.md)
- **Next:** [Section 5: Team Development →](../05-team-development/README.md)
- **Home:** [README](../../README.md)
