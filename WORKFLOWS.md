## Harsimar Kaur

For my workflow, I gave ChatGPT the files from our backend project, including the OpenAPI file and sprint instructions, and told it I wanted to make a frontend bug tracker connected to our deployed backend API. I asked it to create a bug tracker with the fields needed for the POST /issues route so users could submit bug reports.

The first version ChatGPT made worked correctly, but the design was very simple. After testing it, I asked ChatGPT to redesign it with more of a black theme and make the layout look cleaner and more organized. The updated version had a darker theme, cleaner buttons, better spacing, and a more modern design. I mainly relied on AI for the styling, layout, and frontend structure while testing the frontend and making adjustments based on how it looked and functioned.

One issue I ran into was deployment and GitHub branch setup. I accidentally made my frontend branch the default branch for the repository, which caused some confusion while setting up deployment. I also had to set up environment variables so the frontend would connect to our deployed backend API instead of localhost.

Overall, I used a process of prompting, testing, changing things, and asking the AI to improve the frontend until it looked and worked the way I wanted.

---

AI Workflow: Bug Tracker Front-End
Developer: Jonathan Hernandez  
 Agent: Gemini CLI

1. Initial Prompt & Briefing
   Prompt:
   > "I'm not sure how well you are able to read pdfs, but for now, look at sprint5.md and the OpenAPI specs. I want to
   > build a bug tracker front end. Please return with a summary of tasks and any clarifying questions you may have before we
   > begin."

Context Provided:

- sprint5.md (Project requirements)
- openapi.yaml (Backend API contract)
- nextjs.pdf, react-fundamentals.pdf, styling-component-libraries.pdf (Reference materials)

2. The Feedback Loop (Refinement)
   Agent Output:
   The agent summarized the tasks (scaffolding, form implementation, API integration) and asked 5 critical clarifying
   questions regarding styling preferences, success states, validation libraries, deployment targets, and directory
   organization.

User Redirection:

> "I think for styling in particular, we will use MUI. I have no preferences in color. Success state and other states
> should have some visible UI feedback. Not sure about validation, I'd say use Zod. I will deploy to Render. Move the
> existing files into some subdirectory called 'References' and scaffold the app in the root."

3. Execution (The Scaffolding & Build)
   Process:
1. Cleanup: The agent moved all initial files into a /References folder to clear the workspace.
1. Scaffolding: Initialized a Next.js (App Router) project with TypeScript.
1. Dependencies: Installed MUI (@mui/material), Emotion, Zod, and React Hook Form.
1. MUI Integration: Created a ThemeRegistry component to solve the "CSS-in-JS" hydration issue common with Next.js App
   Router and MUI.
1. Schema Design: Created src/lib/validations/issue.ts based on the OpenAPI CreateIssueRequest schema.
1. Form Implementation: Developed BugReportForm.tsx using useForm for state management and fetch for the POST request.

1. Iteration & Bug Fixing
   What went wrong:
   During the npm run build phase, the build failed due to a TypeScript error in the MUI Typography component (the paragraph
   prop was causing a type mismatch in the specific React/MUI version installed).

The Fix:
I prompted the agent to fix the build error. It surgically replaced the problematic prop with sx={{ mb: 2 }}, which
achieved the same visual result while satisfying the TypeScript compiler.

5. What was Kept vs. Cut

- Kept: Next.js App Router (for modern standards), MUI (for rapid professional UI), Zod (for type-safe validation).
- Cut: The default Next.js "Create Next App" landing page and CSS modules were entirely replaced by a clean MUI layout.
  Authentication logic was explicitly excluded per the Sprint 5 MVP requirements.

6. Lessons Learned / "Next Time"

- Proactive Context: Providing the PDFs and OpenAPI spec immediately saved hours of "guessing" the API structure.
- Build Early: Running npm run build early in the process (rather than just relying on npm run dev) was crucial for
  catching the Typography type error before deployment.
- MUI Boilerplate: Next.js App Router requires a bit of "boilerplate" for MUI (the Cache Provider). Next time, I would
  ask the agent to set up the ThemeRegistry as the very first step.

---
