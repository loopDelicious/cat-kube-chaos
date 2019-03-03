This project was originally published in [Deploying a scalable web application with Docker and Kubernetes](link) from the [Postman Engineering blog](https://medium.com/postman-engineering).

### Pre-requisites for local development
1. Download and install [Node.js](https://nodejs.org/en/) and a package manager like [npm](https://www.npmjs.com/), and
1. A container platform like [Docker](https://www.docker.com/get-started).

### For Development

    npm install // install dependencies
    npm start // start app on 3000
    npm run start-server // start server on 5500

### For Production

Create a new file called `.env` located in the root of your project directory. Add your production domain and docker hub username. See the example in `.env.example`. 

If you plan to run Postman tests, then update the `bin/deploy.sh` file by selecting a method of running your Postman tests. To run either of the last 2 options, update your Postman collection UID and environment UID in `bin/deploy.sh` and also add your [Postman API](https://docs.api.getpostman.com/) key to the `.env` file you created in the previous step.

For the deployment, I used a hosted Kubernetes provider called [Kubesail](https://kubesail.com/) that creates a free managed namespace. However, the underlying deployment utility [`npx deploy-to-kube`](https://github.com/kubesail/deploy-to-kube) supports any Kubernetes cluster. By running it inside your app's directory, this utility will automatically generate a Dockerfile, build and push deployment images, generate Kubernetes configuration files, and trigger a deployment on your Kubernetes cluster. 

Run the deployment script

    npm run deploy // run API tests, then deploy frontend and backend to production 

The underlying deployment utility [`npx deploy-to-kube`](https://github.com/kubesail/deploy-to-kube) will prompt you to answer [a series of questions](https://kubesail.com/blog/deploying-node-apps-the-right-way), such as:

    ? What is your application's entrypoint? e.g. src/services/server.js
    ? Which protocol does your application speak? e.g. http

![[catURL website](https://github.com/loopDelicious/cat-kube-stateless/blob/master/catUrl.gif)](https://github.com/loopDelicious/cat-kube-stateless/blob/master/catUrl.gif)
