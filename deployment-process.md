## Deployment Challenges

- Want to deploy each microfrontend independently ( including the container )

- Location of child app remoteEntry.js files must be known at build time!

- Many Frontend deployment solutions assume you are deploying a single project - we need something that can handle multiple different ones

- Probably need a CI/CD pipeline of some sort

- At present, the remoteEntry.js file name is fixed. Need to think about caching issues.

# CI/CD Process

Git Monorepo   |            Github            |                      Action

container           Did Container Change?           Build a production version of container with webpack  --> Upload to Amazon S3
marketing           Did Container Change?           Build a production version of marketing with webpack --> Upload to Amazon S3
            --->                            ---->
dashboard           Did Container Change?           Build a production version of dashboard with webpack --> Upload to Amazon S3
auth                Did Container Change?           Build a production version of auth with webpack --> Upload to Amazon S3



Amazon S3  <-- Amazon CloudFront(CDN) <-- Website


# Workflow for deploying container

Whenever code is pushed to the master/main branch and this commit contains a change to the container folder

Change into container folder

Install dependencies

Create a production build using webpack

Upload the result to AWS S3

## CSS Scoping 

- Custom CSS you are writing for your project
    - Use a CSS-in-JS library
    - Use Vue's built-in component style scoping
    - User Anuglar's built-in component style scoping
    - "Namespace" all your CSS

- CSS coming from a component library or CSS library
    - Use a component library that does css-in-js
    - Manually buid the css library and apply namespacing techniques to it