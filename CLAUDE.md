# Project Rules

## Stack
[your actual stack — vanilla HTML/CSS, or React/Tailwind, etc.]

## Design System
- Font: DM Sans + DM Mono
- All spacing, sizing, and layout values must be taken EXACTLY 
  from Figma — do not estimate or round values
- Do not invent spacing — if Figma says 47px, write 47px
- Use CSS custom properties for all design tokens

## Figma Workflow
- Always call get_design_context before writing any code
- Always call get_variable_defs to extract exact token values
- Implement one section at a time, confirm before moving on
- Never approximate — ask if a value is unclear