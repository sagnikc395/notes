
- how big projects are structured and how to re-use packages
	- multiple parts
	- backend,
	- types and common utilities.
	- multiple frontends
	- generally a single Github repo, contain in the same repo.
	- have multiple modules in our repos.
- before monorepos:
	- why packages / modules ?
		- reusable code
		- people use to shove their repos together in different folders.
		- or different repos for client and server code.
		- npm workspaces made it easier to have client and server code and import code between each other.
	- multiple modules in our repo.
- cal.com:
	- has a bunch of folders 
	- most important things happen in packages and apps folder.
	- apps:
		- has modules 
		- directories.
		- modules are reusable code and seperation of concerns -> each module does what it is supposed to do.
		- emails, onboards etc. -> teams can work independently on modules.
	- breaking big app into small modules.
- zod inference:
	- can make backend code safer by doing input validation and protect from attacks.
	- if the schema changes in the input, then we would have to change the schema in 2 places.
	- given the zod object , can you change the zod inference to typescript without writing additional code.
			- yes ! ; call using types z.infer.
	- trying to write reusable code that can be written in both frontend and backend.
### common:
- common folder that can be shared across.
- common/core -> very small modules that are used by both client and server.
- eg: present even in backpack repo in packages/
- here will write our zod types here 
- create a src/ in common and keep the code here ,so as to differentiate from top level dist/ folder.
- in here src/index.ts has all the types for our app in zod.
- pre mono-repo , we publish our package to npm and other people would pull from it.

## npm.js ->
- registry to put all code that can be used by others.
- we can create and publish our code here.
- common repo locally and things will just work. 
- npm login to authenticate npm.org to login.
- generally prefix name with own account name/repo name
- eg: @sagnikc395/common 
- main should repr where the main index.js file is there and configure and also add a outdir as dist.
- main js file would be pushed.
- not recommended to publishing the ts files, rather push js files. bur created conflcits as types are not given.
- publish using npm publish --access=public .
- npm pack will show us what packages and folders have we actually published.
- .npmignore (root folder) ->
	- add files and folders that we dont want to publish to the registry.
- also again when we publish , need to change the version again , and cannot use the previous verison.

- when we install in client and server , it will give a declaration file does not exist.
- i.e the types for the files are not as it has only .js files.
- we have not published the files for it and we need to create declaration files for it.
## .d.ts ->
- very useful in declaration files.
- just gives the types for the code.
- this contains just the interfaces and the types and not the runtime javascript code.
- enable declarations : true in tsconfig; helpful for others to get our modules as dependency.

## Mono Repos:
- npm workspaces
- lerna 
- turborepo
- rather than using npm, use npm workspaces and with turborepo(mono repo handling repos). without installing anything and can be used.


## Turborepo:
- one of many monorepo frameworks(actually a build system for js and ts)
- can also help us created new monorepo.
- kitchen sink has frontend and backend code also
- can also integrate react-native with it.
- the whole point is to allow one module to import from other module.
- general practice to package these things in signup ui and other.
-  