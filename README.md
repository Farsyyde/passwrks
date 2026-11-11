# PassWrks

**PassWrks** is a free builder toolkit for [ERC-8426](https://eips.ethereum.org/EIPS/eip-8426), the wallet pass extension for NFTs. It turns any NFT into a live Apple Wallet or Google Wallet pass, and PassWrks checks whether a pass actually follows the standard.

Live site: **https://passwrks.com**

## The Pass Checker

The first instrument in the toolkit. Paste a contract address and a token ID, pick a chain, and get a stamped verdict:

- **Conforms** — every MUST check passed
- **Does Not Conform** — at least one MUST check failed
- **Incomplete** — checks were skipped (usually because the pass is gated)

Every report opens with an "In plain English" summary, every check has a plain English line, and the fix-first list shows what to fix in order. No em dashes, no jargon walls.

Current checks: **40**, matching **ERC-8426 SDK 0.4.0** (`@erc8426/core` 0.4.0), including:

- ERC-165 probes (`0xef5f1e71` for the wallet pass interface, `0x470be7e9` for the issuer commitment)
- `passURI` and the manifest, including the manifest `version` MUST check
- Issuer commitment: the manifest's `issuer` compared member for member with the contract's `passIssuer()`
- tokenURI wallet_pass mirror
- Gated 401 / challenge / SIWE / nonce flows
- The equivalent CLI command: `npx erc8426-conformance`

## Try it

- **Pocket** (Robinhood mainnet, chain 4663): contract `0x3a98DE41A0dF554F6b69Ca1b5A1Ad93a745AB1F2`, token `1`
- **WalletChi** (Robinhood testnet, chain 46630): contract `0x96100112afec4a034270d96a133c8952e8c63f45`, token `1`

A gated pass returning 401 is correct behaviour, not a broken pass. The Checker reports it as gated and skips the checks it cannot see behind the login.

## Run it locally

Open `index.html` in a browser. Everything runs client side against the public RPC you pick. No build step, no server, no keys.

## Roadmap

- **Phase 1 — Pass Checker** (live): conformance workbench, 40 checks
- **Phase 2 — Pass Preview / Debugger** (next): render the Apple and Google pass from real manifest data, field by field debugging, and a gated flow simulator so gated passes can be previewed after proving ownership
- **Phase 3 — Issuer Starter Kit**: one click deploy for a conformant issuer

## Pricing

Free for everyone. Paid Pro later, for teams and power users (gated debugging with real wallet login, team workspaces, saved reports, API access).

## Credits

ERC-8426 by [Hunt (@huntclubhero)](https://github.com/huntclubhero), author of the standard and creator of Pocket Pad and WalletChi. PassWrks is independent tooling built on his standard, not a launchpad and not competing with Pocket Pad.

## License

MIT. See [LICENSE](LICENSE).
