## App dependencies

- Node, NodeJS v12.14 or greater up to v14.15.
- npm
- An S3 bucket for hosting frontend app, added bucket policy allowing other AWS services to access the bucket contents.
- A PostgreSQL database to save data
- Environment variables, these are saved in circles ci
- An Elastic Beanstalk environment for hosting backend app
- circleci for continious integration & continious delivery.

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


