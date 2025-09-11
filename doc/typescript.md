# Rules for Writing TypeScript

- Lines must omit trailing semicolons in TypeScript files.
- When writing functions, generally prefer arrow notation instead of a function declarations.  
- When writing methods in classes, prefer arrow functions over function declarations.
- Use `map`, `forEach`, `filter`, and `find` when iterating.
- declare model types using zod validators for example:
  ```TypeScript
  import {z} from zod

  export const myThingValidator = z.object({
    name: z.string(),
    email: z.string().email(),
    createdTimestamp: z.date()
  }).strict()

  export type MyThing = z.infer<typeof myThingValidator>
  ```
  