## Local Deployment

1. Clone [eigen-secret](https://github.com/0xEigenLabs/eigen-secret) and [eigen-secret-ui](https://github.com/0xEigenLabs/eigen-secret-ui), install the deps and build;

```
cd eigen-secret && npm i && npm run build;
cd eigen-secret-ui && npm i && npm run build;
```

2. Launch Node
```
cd eigen-secret;
npx hardhat node
```

3. Launch Server

```
cd eigen-secret;

cp server/.env.sample server/.env
vim server/.env

npm run init:db && npm run server
```

4. Run the CI

```
cd eigen-secret
./test.sh
```

5. Update contract.json and launch the UI service

```
cd eigen-secret-ui;

cp ../eigen-secret/.contract.json src/artifacts/contract.json
npm run serve
```

Open `localhost:8080` in browser and login with Metamask directly.

## Deploy for Production

Check out the [tutorial](https://github.com/0xEigenLabs/eigen-secret/blob/zkpay_dev/script/README.md).
