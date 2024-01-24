# Template Nextjs Blog

| NO  | Tools       | Description |
| --- | ----------- | ----------- |
| 1   | tailwindcss | -           |
| 2   | shadcn/ui   | -           |

## Setup Prisma

1. `yarn add prisma`
2. `npx prisma init` add model to `prisma/schema.prisma` for this project i place my prisma schema on `services/` folder so you must add step 3
3. on package.json add this

```
//other script
//package.json

"prisma" : {
  "schema" : "services/prisma/schema.prisma"
}

//other script
```

sample model

```
//schema.prisma
generator client {
    provider = "prisma-client-js"
}
datasource db {
  provider = "postgresql"
  url = env("POSTGRES_PRISMA_URL") // uses connection pooling
  directUrl = env("POSTGRES_URL_NON_POOLING") // uses a direct connection
}

model Post {
    id String @default(cuid()) @id
    title String
    content String?
    published Boolean @default(false)
    author User? @relation(fields : [authorId], references : [id])
    authorId String?
}

model User {
    id String @default(cuid()) @id
    name String?
    email String? @unique
    createdAt DateTime
    updatedAt DateTime
    posts Post[]
    @@map(name : "users")
}

```

4. install prisma `yarn add prisma`
5. run command `npx prisma` to check if prisma has install properly in our project
6. run command `npx prisma push` to push our model and generate table on our db
7. run command `npx prisma studio` to run prisma UI interface in port 5555
8. install prisma client `npm install @prisma/client` to generate and prepare prisma cleint so can access your database from Next.js using Prisma
9. run command `npx prisma generate`

## Setup Shadcn/UI

1. run command `npx shadcn-ui@latest init`

## Setup NextAuth
