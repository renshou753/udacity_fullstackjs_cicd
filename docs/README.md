
## Infrastructure description

- Node, NodeJS v12.14 or greater up to v14.15.
- npm
- An S3 bucket for hosting frontend app, added bucket policy allowing other AWS services to access the bucket contents.
- A PostgreSQL database to save data
- Environment variables, these are saved in circles ci
- An Elastic Beanstalk environment for hosting backend app
- circleci for continious integration & continious delivery.

##### AWS Cloud Setup

- S3 Frontend: http://udacity-fullstackjs-cicd-tony.s3-website-us-east-1.amazonaws.com/home
- ElasticBeanstalk - Backend: udagram-api-dev.us-east-1.elasticbeanstalk.com
- RDS - Database Host: database-1.cmqpn3dhhub7.us-east-1.rds.amazonaws.com
- RDS - Database Port: 5432
- RDS - Database Name: database-1

## App dependencies

##### Env Variables

```
- POSTGRES_HOST       = <Database_IP_Address>
- POSTGRES_PORT       = <Database_Port>
- POSTGRES_DB         = <Database_Name>
- POSTGRES_USERNAME   = <Database_Username>
- POSTGRES_PASSWORD   = <Database_Password>
- JWT_SECRET          = <Any_PassPhrase>
- AWS_REGION          = <us-east-1>
- AWS_PROFILE         = <Profile>
- AWS_BUCKET          = <Bucket_Name>
```

#### Testing

front:
1. `cd udagram-frontend`
2. `npm run test`
3. `npm run e2e`

backend:

Unit/e2e tests are using the Jasmine Framework.


## Pipeline process

```
    "scripts": {
        "frontend:install": "cd udagram/udagram-frontend && npm install -f",
        "frontend:start": "cd udagram/udagram-frontend && npm run start",
        "frontend:build": "cd udagram/udagram-frontend && npm run build",
        "frontend:test": "cd udagram/udagram-frontend && npm run test",
        "frontend:e2e": "cd udagram/udagram-frontend && npm run e2e",
        "frontend:lint": "cd udagram/udagram-frontend && npm run lint",
        "frontend:deploy": "cd udagram/udagram-frontend && npm run deploy",
        "api:install": "cd udagram/udagram-api && npm install .",
        "api:build": "cd udagram/udagram-api && npm run build",
        "api:start": "cd udagram/udagram-api && npm run dev",
        "api:deploy": "cd udagram/udagram-api && npm run deploy",
        "deploy": "npm run api:deploy && npm run frontend:deploy"
    }
```

From the root of the project:
- `npm run frontend:install`    - To install frontend.
- `npm run frontend:build`      - To build frontend.
- `npm run frontend:lint`       - To lint the frontend.
- `npm run frontend:e2e`        - To test the frontend.
- `npm run frontend:deploy`     - To deploy frontend to s3.
- `npm run api:install`         - To install backend.
- `npm run api:build`           - To build the ts backend.
- `npm run api:deploy`          - To deploy the project to EB.


##### CircleCi

Execution order
- build
- hold
- deploy

The pipeline requires manual approval within the hold phase, after the app is being built. Afterwards the app can be deployed.
