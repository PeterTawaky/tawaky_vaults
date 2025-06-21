---
tags:
  - state-management
  - design-principles
parent: "[[Bloc-Cubit]]"
type: Permanent Note
deeper: 
against: 
---
### this type of decision — whether to:
- Use **a single Cubit Instance** that manages related pieces of state together
- Or **split state** across **multiple Cubit Instances** for better separation between components
### Use Case:
	fetch data but i fetch data from different requests and endpoints, they all shape in one component, how to view this component, should i create different instances of cubit or one cubit to handle this case
___
### 🧠 **1. Single Cubit
 (recommended if data is closely related)**
	If all the API calls are needed to show _one screen_ or _one widget_ at the same time, and they are part of the same logical unit (like a dashboard or profile screen), then using **one Cubit** is usually better.
#### How to do it:
- create a method like `fetchAllData()` which will:
	- Call each endpoint (sequentially or in parallel)
	- Combine the results into one model or state
	- Emit a new state with all data included
___
### 🔀 **2. Multiple Cubits (if data is very independent)**

If the data is **totally unrelated**, and fetched/updated separately, or you're planning to reuse the logic across different screens — then use separate Cubits for each.
- `UserCubit` → handles user data
- `NewsCubit` → handles news data
- Your component listens to both
### ✅ Summary

| Use Case                                           | Cubit Structure     | Notes                         |
| -------------------------------------------------- | ------------------- | ----------------------------- |
| Data feeds one component & is logically connected  | **One Cubit**       | Cleaner, easier to manage     |
| Independent logic or reused across many components | **Multiple Cubits** | Better separation of concerns |
### Related concepts include:
- Separation of concerns
- Feature-based Cubit design
- Reusability of logic
- Centralized vs. Modular Cubits
- Composition of state (how multiple states come together in one UI)
