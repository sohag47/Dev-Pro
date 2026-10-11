# AGENT.md - AI Developer Guide for HeroUI + Next.js

## Project Stack

- Framework: Next.js 14 (App Router)
- Language: TypeScript (strict)
- Styling: TailwindCSS
- UI Library: HeroUI from "@heroui/react" is PRIMARY. shadcn/ui from "@/components/ui" only if HeroUI missing.
- State: Redux Toolkit (Global), useState (Local UI only)
- Form: react-hook-form + zod
- Icons: lucide-react

## Project Structure

/app
/store
store.ts (configureStore)
hooks.ts (useAppDispatch, useAppSelector)
/features
{entity}Slice.ts
/components
/ui (shadcn fallback only)
{Entity}Table.tsx
{Entity}Form.tsx
providers.tsx (HeroUIProvider + Redux Provider)
layout.tsx
page.tsx

## Rules for Agent

### 1. UI Rules (MOST IMPORTANT)

- ALWAYS use HeroUI first: Button, Input, Textarea, Select, Autocomplete, Checkbox, Table, Modal, Card, Chip, Badge, Pagination, Spinner, useDisclosure().
- Patterns:
  - Input: `<Input label="Title" variant="bordered" />`
  - Button: `<Button color="primary">Save</Button>`
  - Table: `<Table><TableHeader><TableColumn><TableBody><TableRow><TableCell>`
  - Modal: `<Modal><ModalContent><ModalHeader><ModalBody><ModalFooter>`
- For Autocomplete, Select, Dropdown ALWAYS pass `disableAnimation`.
- Use HeroUI props (color, variant, size) first, then Tailwind for layout. No custom CSS.

### 2. State Management

- Global data = Redux slice in `app/store/features/`
- State shape: `{ list: T[], selected: T | null, loading: boolean, error: string | null }`
- Use `createSlice` + `createAsyncThunk` for fetch/create/update/delete
- Never use useState for shared data, never fetch directly in component.

### 3. CRUD Pattern

When user says `hero-crud: Entity`:

1. Create slice with thunks
2. Register in store.ts
3. Create Table component with HeroUI Table + Pagination + Search
4. Create Form component with HeroUI Modal + Input + Button
5. Connect to Redux (dispatch fetch on mount, Spinner for loading, Chip color="danger" for error)

### 4. Global Rules - MUST FOLLOW

**a) use client Rule**

- DO NOT add 'use client' blindly.
- First check parent file (layout.tsx, page.tsx, parent component).
- If parent already has 'use client', DO NOT add again in child.
- Only add if this file uses HeroUI / Redux / useState / useEffect AND parent does NOT have it.

**b) Type Safety Rule**

- ALWAYS check types in every file you touch.
- If you find type mistake (any, wrong props, missing interface), you MUST fix it immediately.
- No `any`. Create proper interface.

### 5. Keywords

- `plan: X` -> Give 3-step plan only, no code
- `slice: X` -> Create only Redux slice
- `hero-crud: X` -> Create full CRUD page
- `fix:` -> Explain bug in 1 line Bangla, then fix with HeroUI

## CRITICAL - TERMINAL - NEVER RUN COMMANDS

- NEVER run ANY terminal command unless user explicitly types "run it" or "allow terminal"
- FORBIDDEN (even if you think you should):
  - npm run build, npm run dev, npm run start
  - npm run lint, npm run format, npx tsc, eslint, prettier
  - npm install / yarn / pnpm install
- Your job is ONLY to WRITE FILES. Then STOP.
- Do not verify, build, or check. If you need to suggest a command, write it as text only.

## Git Rule - Global

- NEVER run git add / commit / push / any terminal command
- After completing all tasks in pending-task.md, you MUST append the suggested commit message at the bottom of pending-task.md
- Under "## Suggested Commit" section, write: `feat: [module] - [short work]`
- Example: `feat: attendance - add CRUD and filter`
- Do not create new file, just update pending-task.md bottom line
- I will commit manually
