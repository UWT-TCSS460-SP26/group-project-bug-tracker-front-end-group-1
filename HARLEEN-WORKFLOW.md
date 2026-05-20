# Harleen Sprint 5 AI Workflow Writeup

## First Prompt

I started by giving the AI agent my Sprint 5 context file and the team's OpenAPI spec. My first prompt asked it to build a Next.js public bug report form for `POST /issues`.

The form needed four fields:
- title
- description
- stepsToReproduce
- reporterEmail

I also told the agent to use `NEXT_PUBLIC_API_URL` instead of hardcoding the backend URL.

## What the Agent Built First

The agent created a Next.js form with the correct four fields. It used React state to store the form data and used `fetch` to submit the form to the backend.

It also added basic UI feedback for success and errors.

## What Worked

The first version had the correct form fields and submitted the right request body shape for the backend. The page was simple and focused only on the public bug report form, which matched the sprint requirement.

## What Needed Fixing

The first issue was that the input text was too light and hard to read. I prompted the agent to make the input and textarea text darker.

The second issue was that errors were showing as `{}` instead of a readable message. I prompted the agent to improve the error handling so it would show clear messages like `title is required`, `description is required`, or the backend error message.

## What I Tested

I tested the form with the deployed backend API:

`https://tcss460-team-1-api.onrender.com`

I verified that a direct curl request to `POST /issues` returned `201 Created`.

I also tested the frontend form and saw a success message after submitting a bug report.

## What I Kept

I kept the single-page form structure, the four fields from the OpenAPI spec, the environment variable setup, and the simple Tailwind styling.

## What I Changed

I changed the form styling so typed text was readable. I also improved the error handling so the user does not see confusing output like `{}`.

## What I Would Do Differently Next Time

Next time, I would give the AI agent an example successful backend response and an example validation error response at the beginning. That would probably help it build better error handling on the first try.