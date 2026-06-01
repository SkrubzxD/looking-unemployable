So it seems Deployment CI/CD is correlated with Github Actions, even GitLab(Probably Ona now).

## The templates can be run, make a yaml file
- If we happen to push code, we want to deploy, or pull and test. These are called 'triggers'. These look kinda like Docker Files
```
# test.yaml

name : Github Actions test

on: 
	pull_request:
		branches:
			- main
			  
jobs:
	tests:
		runs-on:ubuntu-latest
		container: 
			image: node: 20
		steps: 
			- uses: actions/checkout
			- with:
			  node-version: 20
			- run: npm run dev
			- run: npm run test
			  
```


```
# deploy.yml

name: Github Actions deploy
on:
	push:
		branches:
			- main
	
	jobs:
		deploy:
			runs-on:ubuntu-latest
			container:
				image: node: 20
			steps:
				- uses: action/checkout@v3
				  with:
					  node-version: 20
				- run: npm run build
				- name: Get SSH and set perms
					  run: 
						  mkdir -p ~/.ssh
						  echo "${{ secrets.SSH_PRI_KEY }}" > ~/.ssh/id_rsa && chmod 600 ~/.ssh/id_rsa
				- name: Deploy
					run: scp -o #Somethingsomething
```

And maybe add Keys in Actions Secret

We can also use Docker to replicate this.
