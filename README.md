![UNOstr](/unostr.jpg)

# UNOstr

UNOstr is a serverless [Nostr](https://github.com/fiatjaf/nostr) relay purpose-built for [Cloudflare Workers](https://workers.cloudflare.com/) that ONLY requests events from all online relays using the nostr.watch [API](https://api.nostr.watch/). 

This relay relay will stream as many possible events from as many possible online relays. This relay does NOT support saving or blasting events.

### Dependencies

UNOstr requires the [@noble/curves](https://github.com/paulmillr/noble-curves) package for cryptographic operations and the [@evanw/esbuild](https://github.com/evanw/esbuild) bundler:

```
npm install @noble/curves
npm install -g esbuild
```

### Building

Clone the repo to your machine and open `worker.js` in a file editor. Edit the contents of `relayInfo` and `relayIcon` as desired to customize the relay name, icon, etc.
 
*Optional:*
- Edit the `nip05Users` section to add usernames and their hex pubkey for NIP-05 verified Nostr address.

We'll use `esbuild` to bundle the worker script:

```
esbuild worker.js --bundle --outfile=dist/worker.js --platform=neutral --target=es2020
```

The command assumes you're in the same directory as the `worker.js` file.

### Deployment

You can deploy UNOstr either directly through the Cloudflare dashboard or through Wrangler CLI:

#### Cloudflare Dashboard

1. Log in to your Cloudflare dashboard.
2. Go to the Workers section and create a new worker. You can call it whatever you'd like.
3. Copy the contents of `dist/worker.js` and paste into the online editor. See the `example.js` file in this repo for what a successfully bundled file should look like.
4. Save and deploy the worker.
5. Add a custom domain in Worker's settings (this will be the desired relay URL).

#### Wrangler CLI

1. Configure your `wrangler.toml` with your Cloudflare account details.
2. Publish the worker:

```
wrangler publish
```
3. Add a custom domain in Worker's settings (this will be the desired relay URL).

## Usage

Once deployed, you can either use the Cloudflare Worker's default "workers.dev" endpoint URL or a custom domain, adding it to any Nostr client using the secure websocket protocol.

Example:

- `wss://unostr.example.workers.dev/`

## Contributing

Contributions to UNOstr are welcome! Please submit issues, feature requests, or pull requests through the project's [GitHub repository](https://github.com/Spl0itable/unostr).

## License

UNOstr is open-sourced software licensed under the MIT license.

## Contact

For inquiries related to UNOstr, you can reach out on Nostr at `npub16jdfqgazrkapk0yrqm9rdxlnys7ck39c7zmdzxtxqlmmpxg04r0sd733sv`
