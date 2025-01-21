## Understanding Monorepos

- Monorepo is a code repo that contains the source code for multiple applications and packages.

```
- package.json
- pnpm-lock.yaml
- README.md
- apps
    - docs
    - mobile
    - web
- packages
    - logger
    - ui
    - utils
- tooling
    - eslint-config
    - prettier-config
```

- In monorepo, we will create organizational structures for our code where we can share "packages" to many applications.
- This creates better DX, shipping velocity -> better applications.
- In monorepo , we can gurantee that changes are atomic and that we know exactly what source code we are deploying.
- Helps in shipping faster and allows us to work together much more quickly.

## Monorepo != Monolith

- Various applications in our monorepo can(and should!) act independently of each other.
- Making changes to our web application doesnt have to force our mobile application to redeploy.

```
- package.json
- pnpm-lock.yaml
- apps
    - nextjs (A monolith)
    - vite (A frontend)
    - express (A backend)
```

-
