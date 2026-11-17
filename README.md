# Design Factory: front end

Web front end for **Design Factory**, a platform for learning software design patterns, built as my MBA capstone project (TCC) in Software Engineering at USP/ESALQ.

Students sign up, follow guided learning tracks, write and run Java code right in the browser, and answer a quiz at the end of each track. The API lives in [design-patterns-factory-backend](https://github.com/guerrasz/design-patterns-factory-backend).

> The course content is in Brazilian Portuguese.

## Features

- **Learning tracks:** an introduction track plus one track each for the **Factory**, **Adapter** and **Singleton** patterns, with six lessons per pattern track
- **In-browser Java editor:** a Monaco editor with a console that runs your code through the [Piston](https://github.com/engineer-man/piston) code execution API
- **Quizzes** to close each pattern track
- **Progress tracking:** per-track progress bars and experience points on the profile page
- **Accounts:** sign-up, login and a cookie-based session

## Stack

- Next.js 15 (App Router) and React 19
- TypeScript
- Tailwind CSS 4 and shadcn/ui (Radix UI)
- React Hook Form and Zod for form validation
- Monaco Editor
- Axios
- Docker (standalone Next.js output)

## Project structure

```
src/
├── app/
│   ├── api/          Route handlers: login, signup, session, class progress
│   ├── tracks/       intro, factory, adapter and singleton tracks, lessons and quizzes
│   ├── login/  signup/  profile/
│   └── page.tsx      Home
├── components/
│   ├── internal/     Code editor, console, runner, quiz, track and lesson components
│   └── ui/           shadcn/ui components
├── _clients/         backend.ts (Spring Boot API) and piston.ts (code execution)
└── _utils/           Session handling and progress calculation
```

## Running locally

You need Node.js 22 and the [backend](https://github.com/guerrasz/design-patterns-factory-backend) running on port 8080.

```bash
npm install
API_ENDPOINT=localhost npm run dev
```

Then open http://localhost:3000.

`API_ENDPOINT` is the hostname of the API; the app calls `http://$API_ENDPOINT:8080`.

### Full stack with Docker Compose

The backend repository has a `compose.yml` that starts PostgreSQL, the API and this front end together:

```bash
git clone https://github.com/guerrasz/design-patterns-factory-backend
cd design-patterns-factory-backend
docker compose up
```

## Building the image

```bash
docker build -t next-designfactory .
docker run -p 3000:3000 -e API_ENDPOINT=<api-host> next-designfactory
```
