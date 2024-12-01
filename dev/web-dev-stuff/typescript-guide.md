# Modern Full-Stack TypeScript Development Guide

## Table of Contents
1. [Getting Started with TypeScript](#getting-started)
2. [Tech Stack Overview](#tech-stack)
3. [Prisma ORM Guide](#prisma)
4. [tRPC Implementation](#trpc)
5. [Learning Resources](#resources)

## Getting Started with TypeScript {#getting-started}

### Core Stack Components
- **Next.js**: React framework with TypeScript support
- **Tailwind CSS**: Utility-first CSS framework
- **Prisma**: Type-safe ORM
- **tRPC**: End-to-end type-safe API layer
- **PostgreSQL**: Database

### Learning Timeline
1. **TypeScript Fundamentals (2-3 days)**
   - Types and interfaces
   - Generics
   - Type inference
   - Union and intersection types

2. **React with TypeScript (1 week)**
   - Components and Props typing
   - Hooks with TypeScript
   - State management
   - Event handling

3. **Next.js (1-2 weeks)**
   - File-based routing
   - API routes
   - Server components
   - Data fetching patterns

## Tech Stack Overview {#tech-stack}

### Frontend (Next.js)
```typescript
// Example of a typed component
interface UserProps {
  name: string;
  email: string;
  role: 'admin' | 'user';
}

const UserCard: React.FC<UserProps> = ({ name, email, role }) => {
  return (
    <div className="p-4 bg-white shadow rounded">
      <h2>{name}</h2>
      <p>{email}</p>
      <span>{role}</span>
    </div>
  );
};
```

### Backend Setup
```typescript
// Example server setup with Express
import express from 'express';
import { PrismaClient } from '@prisma/client';

const app = express();
const prisma = new PrismaClient();

app.use(express.json());
```

## Prisma ORM Guide {#prisma}

### Schema Definition
```prisma
// schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

### Common Operations
```typescript
// Create
const user = await prisma.user.create({
  data: {
    email: 'user@example.com',
    name: 'John Doe',
  },
});

// Read with relations
const users = await prisma.user.findMany({
  include: {
    posts: true,
  },
});

// Update
const updatedUser = await prisma.user.update({
  where: { id: 1 },
  data: { name: 'Jane Doe' },
});

// Delete
const deletedUser = await prisma.user.delete({
  where: { id: 1 },
});
```

## tRPC Implementation {#trpc}

### Basic Setup
```typescript
// server/trpc.ts
import { initTRPC } from '@trpc/server';

const t = initTRPC.create();

export const router = t.router;
export const publicProcedure = t.procedure;
```

### Creating Procedures
```typescript
// server/routers/user.ts
import { z } from 'zod';
import { router, publicProcedure } from '../trpc';

export const userRouter = router({
  getUser: publicProcedure
    .input(z.number())
    .query(async ({ input, ctx }) => {
      return ctx.prisma.user.findUnique({
        where: { id: input },
      });
    }),
  
  createUser: publicProcedure
    .input(z.object({
      email: z.string().email(),
      name: z.string(),
    }))
    .mutation(async ({ input, ctx }) => {
      return ctx.prisma.user.create({
        data: input,
      });
    }),
});
```

### Client Usage
```typescript
// Frontend component
const UserProfile = () => {
  const { data, isLoading } = trpc.user.getUser.useQuery(1);

  if (isLoading) return <div>Loading...</div>;
  
  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.email}</p>
    </div>
  );
};
```

## Learning Resources {#resources}

### TypeScript & Next.js
- Official TypeScript documentation: https://www.typescriptlang.org/docs/
- Next.js documentation: https://nextjs.org/docs
- React TypeScript Cheatsheet: https://react-typescript-cheatsheet.netlify.app/

### Prisma Resources
- Official Prisma documentation: https://www.prisma.io/docs
- Prisma Examples Repository: https://github.com/prisma/prisma-examples
- Video Tutorial by Traversy Media: https://www.youtube.com/watch?v=RebA5J-rlwg

### tRPC Resources
- Official tRPC documentation: https://trpc.io/docs
- Create T3 App: https://create.t3.gg/
- Tutorial by Theo: https://www.youtube.com/watch?v=2LYM8gf184U

### Additional Tools
- Create T3 App (recommended starter): https://create.t3.gg/
- TypeScript ESLint: https://typescript-eslint.io/
- Zod (TypeScript-first schema validation): https://zod.dev/

---

*Note: This guide assumes basic JavaScript knowledge and some familiarity with React. URLs and resources mentioned should be verified as they may change over time.*
