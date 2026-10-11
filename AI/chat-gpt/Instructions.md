# PROJECT: ITL-Frontend

Stack: Next.js 14 App Router, TypeScript, TailwindCSS, HeroUI (MAIN), shadcn/ui (only if HeroUI missing), Redux Toolkit, React Hook Form + Zod

## Folder Structure

- app/store/store.ts -> Redux store config
- app/store/features/*Slice.ts -> All slices
- app/components/* -> UI components
- app/providers.tsx -> HeroUIProvider + Redux Provider

## ABSOLUTE RULES

### 1. UI Library Priority

- ALWAYS use HeroUI from @heroui/react FIRST.
- Components: Button, Input, Textarea, Select, Autocomplete, Checkbox, Table, Modal, Card, Chip, Pagination, Spinner.
- Only if HeroUI component does NOT exist, use shadcn from @/components/ui.
- Styling: Use HeroUI props (color="primary", variant="bordered", size="sm") first, then Tailwind for layout (flex, grid, gap).
- For Autocomplete, Select, Dropdown ALWAYS pass disableAnimation.

### 2. HeroUI Patterns

- Button: <Button color="primary" variant="solid">
- Input: <Input label="Name" variant="bordered" />
- Table: <Table><TableHeader><TableColumn><TableBody><TableRow><TableCell>
- Modal: <Modal><ModalContent><ModalHeader><ModalBody><ModalFooter> + useDisclosure()
- CRUD Combo: Table + Top Search Input + Add Button + Modal Form + Pagination

### 3. State Management

- Global data = Redux Toolkit slice in app/store/features/ with createSlice + createAsyncThunk
- State shape: { list: T[], selected: T | null, loading: boolean, error: string | null }
- Local UI state = useState
- Export typed hooks: useAppDispatch, useAppSelector

### 4. Global Rules - MUST FOLLOW

a) use client Rule - CHECK PARENT FIRST

- DO NOT add 'use client' blindly to every component.
- First check parent file (layout.tsx, page.tsx, or parent component).
- If parent already has 'use client', DO NOT add it again in child.
- Only add if component uses HeroUI / Redux / useState / useEffect AND parent does NOT have it.

b) Type Safety Rule

- ALWAYS check types in every file you touch.
- If you find type mistake (any, wrong props), you MUST fix it immediately.
- No any. Create interface.

c) Git Rule - Global

- After completing ALL tasks in pending-task.md, you MUST update bottom section "## Suggested Commit" in pending-task.md
- Format: feat: [module] - [short work]

### 5. Keywords

- plan: X -> Only give 3-step plan, no code
- slice: X -> Create only Redux slice
- hero-crud: X -> Create full CRUD page with HeroUI Table + Modal + Redux
- fix: -> Explain bug in 1 line Bangla, then fix code
