# Lesson 15 in Patrick's course with Moralis front end

In this section we use moralis backend to make the front end easier to build. Moralis provides a database, cloud functions, listen and indexes event of our protocol so we can display that information in the front end easily and saving gas in the process.

Some point that I want to remember:

- The period at the end is important it creates the project in the same directory: `yarn create next-app .`

- Try to not change (much) the protocol for the website

- We used a fast reverse proxy to expose the local blockchain to Moralis Servers, use the `moralis-admin-cli` to connect to the moralis server, pretty cool.

- We use the moralis servers with our local blockchain.

Steps to working with moralis servers:

1. run local hardhat network
2. connect to moralis using: `yarn moralis:sync`, we should be "connected" in the front end of Moralis admin page.
3. now run: `node addEvents.js` this will add the events that we want to listen to Moralis programatically
   now we mint and list using a script: `hh run scripts/mint-and-list-item.js --network localhost`
4. Now we have to use Moralis cloud functions to update the database every time an event happens in the local blockchain with. By running `yarn moralis:cloud` we update our cloud functions to moralis

- How to call a function from a contract using `react-moralis`

```js
const { runContractFunction: buyItem } = useWeb3Contract({
  abi: nftMarketplaceAbi,
  contractAddress: marketplaceAddress,
  functionName: 'buyItem',
  msgValue: price,
  params: {
    nftAddress: nftAddress,
    tokenId: tokenId,
  },
})
```

To transform from ETH to wei and make a transaction

```js
const price = ethers.utils
  .parseUnits(data.data[2].inputResult, 'ether')
  .toString()
```

- Remember to get the chainId from moralis (parse it to string) and
  the adressess that you are going to need

```js
const { chainId, account, isWeb3Enabled } = useMoralis()
const chainString = chainId ? parseInt(chainId).toString() : '31337'
const marketplaceAddress = networkMapping[chainString].NftMarketplace[0]
```

Patrick is **aaaawesome!**

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
