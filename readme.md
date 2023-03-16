# PrismaClient commands

### Imports and sets
~~~typescript
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();
~~~


### create -> Insert a data
~~~typescript
async function main() {
  await prisma.user.create({
    data: {
      name: 'Kamile',
      email: 'kamile@prisma.io',
      posts: {
        create: { title: 'Hello World'},
      },
      profile: {
        create: { bio: 'Incrivelmente incrivel'}
      },
    },
  })
~~~

### findMany - Read data
~~~typescript
  const allUsers = await prisma.user.findMany({
    include: {
      posts: true,
      profile: true,
    }
  })
  console.dir(allUsers, { depth: null })
}

main()
  .then(async () => {
    await prisma.$disconnect()
  })
  .catch(async (e) => {
    console.error(e)
    await prisma.$disconnect()
    process.exit(1)
  })
~~~

### update - update a data
~~~typescript
async function main() {
  const post = await prisma.post.update({
    where: { id: 1 },
    data: { published: true },
  })
  console.log(post)
}
~~~
