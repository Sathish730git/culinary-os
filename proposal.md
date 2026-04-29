# Culinary OS – Enhancement Proposal

## 1. Current System (Existing Application)

The Culinary OS application is already built and includes the following:

### Dashboard
- Shows Brands count
- Shows Branches count
- Shows Users
- Shows Dishes
- Shows Ingredients
- Shows Tools

### Available Modules
- Dishes
- Feedback
- Dish Categories
- Ingredients
- Tools
- Media Library
- Dish Proposals
- History

### Current Behavior
- Dishes can be created
- Ingredients are available but not fully structured
- No stage-wise cooking steps
- No strict accompaniment mapping
- No structured publishing workflow

---

## 2. Current Problems / Limitations

- Ingredients are not linked with brand and branch properly
- No step-by-step cooking stage tracking
- No video upload during preparation steps
- Tools are not categorized (cutlery vs others)
- Accompaniments are not enforced as side dishes
- No festival-based menu classification
- Chef notes are not clearly visible
- No explanation for “what can go wrong”
- No controlled publishing (Test Kitchen role missing)

---

## 3. Required Changes (New Enhancements)

### 1. Ingredients Section
- Add Brand selection
- Add Branch mapping
- Each ingredient must belong to a branch

### 2. Stage Steps
- Add new tab after presentation
- Show ingredients as checklist
- Allow video upload for preparation

### 3. Tools Classification
- Add categories (cutlery, cooking tools, etc.)

### 4. Accompaniment Mapping
- Must be mapped as side dish
- Display in overview:
  "Served with <name> as a side dish"

### 5. Alternative Ingredients
- Provide substitute options

### 6. Festival Menu
- Add new tab under Dish Category

### 7. Premium Ingredients
- Show imported ingredients with brand, photos, videos

### 8. Failure Explanation
- Show "What can go wrong" in each step

### 9. Chef Note
- Must be displayed in overview

### 10. Default Portion
- Set default value = 2

### 11. Test Kitchen Publishing
- Only Test Kitchen can publish after R&D completion