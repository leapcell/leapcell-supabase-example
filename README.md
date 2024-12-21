# Leapcell Supabase Example

Supabase is an open-source Firebase alternative, providing developers with a powerful and scalable backend.

## Getting Started

1. Create a Supabase account.
2. Go to the [Supabase Dashboard](https://supabase.com/dashboard/projects) and click `New Project`.
3. Once the project is created, open it.

Click the `Connect` button at the top of the interface (it might be hard to spot, located at the very top of the page). 

Ensure you select the **Transaction Pooler** option for the connection. You will see a connection string similar to the following:

```
postgresql://postgres.**********:[YOUR-PASSWORD]@aws-0-us-east-1.pooler.supabase.com:6543/postgres
```

You can use this connection string with popular ORMs or directly in your code.

---

## Example Usage

### Using Node.js (Prisma ORM)
1. Install Prisma:
   ```bash
   npm install prisma @prisma/client
   ```
2. Initialize Prisma:
   ```bash
   npx prisma init
   ```
3. Update your `prisma/schema.prisma` file:
   ```prisma
   datasource db {
     provider = "postgresql"
     url      = "postgresql://postgres.**********:[YOUR-PASSWORD]@aws-0-us-east-1.pooler.supabase.com:6543/postgres"
   }

   generator client {
     provider = "prisma-client-js"
   }

   model User {
     id    Int    @id @default(autoincrement())
     name  String
     email String @unique
   }
   ```
4. Run migrations and use the database:
   ```bash
   npx prisma migrate dev
   ```

---

### Using Python (Django ORM)
1. Install dependencies:
   ```bash
   pip install django psycopg2-binary
   ```
2. Update your `settings.py` in the Django project:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': 'postgres',
           'USER': 'postgres.**********',
           'PASSWORD': '[YOUR-PASSWORD]',
           'HOST': 'aws-0-us-east-1.pooler.supabase.com',
           'PORT': '6543',
           'OPTIONS': {
               'sslmode': 'require',
           },
       }
   }
   ```

---

### Using Node.js Without an ORM
1. Install the `pg` library:
   ```bash
   npm install pg
   ```
2. Connect to Supabase:
   ```javascript
   const { Client } = require('pg');

   const client = new Client({
     connectionString: "postgresql://postgres.**********:[YOUR-PASSWORD]@aws-0-us-east-1.pooler.supabase.com:6543/postgres",
   });

   client.connect()
     .then(() => console.log('Connected to Supabase'))
     .catch(err => console.error('Connection error', err.stack));
   ```

---

### Using Python Without an ORM
1. Install `psycopg2`:
   ```bash
   pip install psycopg2
   ```
2. Connect to Supabase:
   ```python
   import psycopg2

   connection = psycopg2.connect(
       dbname="postgres",
       user="postgres.**********",
       password="[YOUR-PASSWORD]",
       host="aws-0-us-east-1.pooler.supabase.com",
       port="6543",
       options="-c sslmode=require"
   )

   print("Connected to Supabase")
   ```

Now you're ready to use Supabase for your application with Node.js or Python! 🎉
