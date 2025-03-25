# Fastify@4 issue When building with typescript@4.7

## Versions

node : 22.14.0
npm: 10.9.2
fastify: 4.29.0
typescript: 4.7.4
@types/node :20.14.8

## Steps to reproduce

Run the below commands to create the app.

```
mkdir fastify-app 
cd fastify-app 

nvm install 
nvm use lts/jod 

npm init –y 

npm i fastify@4 
npm i -D typescript@4.7 @types/node@20.14.8 
```
Add the below scripts in the `package.json` file

```
{ 
 "scripts": { 
 "build": "tsc" 
 } 
} 
```

Then run 

``` 
npx tsc –init 
```
Disable the skipLibCheck in `tsconfig.json` file

```
"skipLibCheck": false 
```
 
Create `index.ts`file and add the following in the root directory

```
import Fastify from 'fastify'; 

const fastify = Fastify(); 

const start = async () => { 
  try { 
    await fastify.listen({ port: 3000, host: '0.0.0.0' }); 
  } catch (err) { 
    fastify.log.error(err); 
    setTimeout(() => { 
      process.exit(1); 
    }, 1000); 
  } 
}; 

start(); 
```

Then the build
 ```
npm run build 
```

## Error

```
node_modules/fastify/types/route.d.ts:145:9 - error TS1005: ')' expected.

145     path: string,
            ~

node_modules/fastify/types/route.d.ts:147:3 - error TS1128: Declaration or statement expected.

147   ): FastifyInstance<RawServer, RawRequest, RawReply, Logger, TypeProvider>;
      ~

node_modules/fastify/types/route.d.ts:147:4 - error TS1128: Declaration or statement expected.

147   ): FastifyInstance<RawServer, RawRequest, RawReply, Logger, TypeProvider>;
       ~

node_modules/fastify/types/route.d.ts:148:1 - error TS1128: Declaration or statement expected.

148 }
    ~


Found 303 errors in 2 files.

Errors  Files
   285  node_modules/fastify/types/instance.d.ts:205
    18  node_modules/fastify/types/route.d.ts:135

```