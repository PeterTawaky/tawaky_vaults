---
type: Fleeting Note
tags:
  - "#api"
created_at: 2025-04-09 05:35
---
### What is Pagination?
**Pagination** is the process of **breaking up a large set of data into smaller parts**, and loading them in **steps or pages** instead of all at once.

### Why Pagination?
If you're working with a large dataset, sending all records in one API response is:
- **Inefficient** (too much data)
- **Slow** (heavy load on server & client)
- **Hard to manage** on mobile/low bandwidth
So instead, we load like:
- Page 1 → 20 posts
- Page 2 → next 20 posts (when user scrolls down)
- Page 3 → another 20, and so on…

## Example in Real Life
Like when you:
- Scroll down Facebook or Instagram and it loads more posts
- Browse products on Amazon or `Jumia` — and more appear when you scroll or click “Next Page”

## Types of Pagination
1. **Offset Pagination**
    - `?page=2&limit=20` → skip the first 20, get the next 20
    - Easy, but not perfect for fast-changing data
2. **Cursor-Based Pagination**
    - `?after=post_id_123` → get posts _after_ that ID
    - Better for live or dynamic data (e.g., social media)