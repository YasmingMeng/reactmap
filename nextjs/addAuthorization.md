<!--
 * @Description:
 * @Date: 2024-11-20 10:47:10
 * @LastEditTime: 2024-11-21 10:50:42
-->

## How to add Authorization for Web Application

1. Install NextAuth.js
   ```json
   pnpm i next-auth@beta
   ```
2. generate openssl key
   ```json
   openssl rand -base64 32
   ```
   and add `AUTH_SECRET=your-secret-key` into the .env file
3. create name as `auth.config.ts` file into the root menu

```typescript
import type { NextAuthConfig } from 'next-auth'

export const authConfig = {
  pages: {
    signIn: '/login',
  },
  callbacks: {
    authorized({ auth, request: { nextUrl } }) {
      const isLoggedIn = !!auth?.user
      const isOnDashboard = nextUrl.pathname.startsWith('/dashboard')
      if (isOnDashboard) {
        if (isLoggedIn) return true
        return false // Redirect unauthenticated users to login page
      } else if (isLoggedIn) {
        return Response.redirect(new URL('/dashboard', nextUrl))
      }
      return true
    },
  },
  providers: [], // Add providers with an empty array for now
} satisfies NextAuthConfig
```

4. create a file called `middleware.ts`, then import `authConfig` object. By utilizing NextAuth.js, middleware can prevent routes rendering until the authorization is fully verified.
5. password hashing: using the bcrypt package to converts a password into fixed-length characters, allowing for comparison and matching with the password stored in the database.

- create a file called `auth.ts`, and construct an authenticate function, writing separately into both the auth.ts and action.ts
