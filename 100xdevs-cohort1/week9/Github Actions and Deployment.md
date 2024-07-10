- How to deploy backend on the internet
- not the end state of depolyment but the start.
- go from aws to github actions.
- apps deployed on aws:
	- bare minimum of becoming a full stack engineer.
- devops/devtooling as a field:
	- super lucrative
	- super chill
	- can do a lot by doing very little

### Pre CI/CD Days:
- No concept of automatic deployments
- whenever your push to github, we can also pull your code to the server. (ssh into the server and pull from there).
### Why only backend ?
- frontend deployment is easy (vercel/netlify)
- Frontend:
	- Just builds into HTML/CSS/JS and distribute them via CDN.
	- solved problems.
- Why backend hard ?
	- every user gets different response, whereas everyone gets the same HTML/CSS/JS(until we reach next)
	- harder and more expensive to deploy.
### High Level Steps to deploy Backend:
afaik dumb way
1. Choosing a cloud provider(aws/gcp/azure)
2. creating a instance 
3. getting a ssh key
4. opening firewalls on the machine port 80/443/22 (3000/3001?)
5. Cloning your code to the machine.
6. Installing node/npm (why docker is useful?)
7. Building and running code(pm2?)
8. pointing your domain to the server 
9. using nginx to setup a reverse proxy
10. certificate management -> https://

