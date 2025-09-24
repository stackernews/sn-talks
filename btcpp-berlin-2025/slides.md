---
title: Challenges of Building a Non-Custodial Lightning App
author: ek
theme: Warsaw
date: October 3, 2025
---

# Agenda

1. Why Non-Custodial?
2. Custodial vs Non-Custodial Architecture
3. User Experience
4. Challenges

---

\center{\textbf{\underline{Why Non-Custodial?}}}

::: notes

in late 2023, I gave a talk and pointed out that I wasn't sure about the legality of everything SN did (which I honestly wasn't), then someone in the audience that ran an exchange circa 2013 came up to me after and told me SN was most definitely breaking the law - specifically money transmission laws. Then WoS pulled out of the US. Then samourai was indicted. So we started talking to lawyers, legal counsel for other bitcoin companies, and other bitcoin founders and confirmed it: to run a custodial bitcoin service in the US, you need money transmitter licenses in all the states that require them (most states) and register with the federal government as a money service business. Not only would this cost millions of dollars and take years and be near impossible in states like New York, but it would also mean needing to KYC our customers and monitor and report to the government about them. This also doesn't only apply to the US - most countries have similar laws. So we said "fuck that."

:::

---

# Wallet of Satoshi stopped serving US customers

![](img/wos.png)

\tiny https://www.nobsbitcoin.com/wallet-of-satoshi-stops-serving-us-customers/

---

# Samourai Devs prosecuted

![](img/samourai_charged.png)

\tiny https://www.justice.gov/usao-sdny/pr/founders-and-ceo-cryptocurrency-mixing-service-arrested-and-charged-money-laundering

---

# Phoenix Wallet stopped serving US customers

![](img/phoenix.png)

\tiny https://www.nobsbitcoin.com/phoenix-wallet-to-be-removed-from-us-app-stores-on-may-3/

---

# New York's BitLicense ...

![](img/coinbase_bitlicense.png)

\tiny https://www.coinbase.com/en-de/blog/coinbase-obtains-the-bitlicense

# ... is not enough for the Lightning Network

![](img/coinbase_ln.png)

\tiny https://bitcoinmagazine.com/business/coinbase-integrates-bitcoin-lightning-for-100-million-users

---

# Alternatives

\center{\textbf{Paying \$\$\$ for the privilege to:}}

* implement KYC
* monitor transactions
* report suspicious activity

---

# Alternatives

\center{\textbf{``Soft KYC''}}

\includegraphics[width=0.4\textwidth,keepaspectratio]{img/soft-kyc.png}

::: notes

* balance between customer convenience and regulatory compliance
* does not immediately verify information

:::

---

\center{\textbf{We said no.}}

---

# OFAC

\center{\textbf{... but still had to comply with OFAC sanctions ...}}

::: notes

Office of Foreign Asset Control

:::

---

# OFAC

\begin{quote}
All U.S. persons must comply with OFAC sanctions, including all U.S. citizens and permanent residents regardless of where they are located, all individuals and entities within the United States, and all U.S. incorporated entities and their foreign branches.
\end{quote}

\center{\tiny https://ofac.treasury.gov/faqs/11}

---

# OFAC

![](img/ofac.png)

\tiny https://github.com/stackernews/stacker.news/commit/a5e50821b7e0dba0400a5f8ada6d3741a92de9d3

---

\center{\textbf{\underline{Custodial vs Non-Custodial Architecture}}}

---

# Custodial Architecture

- "zaps" are database transactions
- only deposits and withdrawals are lightning payments
- lightning node can go down and most users wouldn't notice

\center{\textbf{Is this really a lightning app?}}

---

# Non-Custodial Architecture

- (almost) every payment is over lightning
- senders now have to pay routing fees[^1]
- zaps need to be forwarded to receiver

\center{\textbf{How to never take custody of funds while forwarding?}}

[^1]: if they don't have a channel with SN

---

# lnproxy

![](img/lnproxy.png)

---

# lnproxy

\center{\textbf{Demo}}

---

\center{\textbf{The End.}}

---

\center{\textbf{I wish ...}}

---

\center{\textbf{\underline{User experience}}}

---

# QR codes are not good UX

![](img/qr.png)

::: notes

- desktop vs mobile
- everything about a payment can be slow
  - requesting an invoice
  - paying
  - forwarding
  - settling

:::

---

# QR codes are not good UX

- desktop vs mobile
- everything about a payment can be slow

\center{\textbf{What if the payment fails?}}

---

# Wallets

![](img/wallets.png)

---

# Wallets

\center{\textbf{Demo}}

---

# Payment UX

- optimistic payments
- retry payments in the background
- notify user if a payment failed

\center{\textbf{should \textit{feel} like custodial}}

---

# Payment retries

- payments are attempted three times
- users can attach multiple wallets as fallbacks
- did sender or receiver fail?

\center{\textbf{Never reuse a lightning invoice!}}

---

# P2P zaps

![](img/p2p-zaps/001.png)

---

# P2P zaps

![](img/p2p-zaps/002.png)

---

# P2P zaps

![](img/p2p-zaps/003.png)

---

# P2P zaps

![](img/p2p-zaps/004.png)

---

# P2P zaps

![](img/p2p-zaps/005.png)

---

# P2P zaps

![](img/p2p-zaps/006.png)

---

# P2P zaps

![](img/p2p-zaps/007.png)

---

# P2P zaps

![](img/p2p-zaps/008.png)

---

# P2P zaps

![](img/p2p-zaps/009.png)

---


# P2P zaps

![](img/p2p-zaps/010.png)

---

# P2P zaps

![](img/p2p-zaps/011.png)

---

# P2P zaps

![](img/p2p-zaps/012.png)

---

# P2P zaps

![](img/p2p-zaps/013.png)

---

# P2P zaps

![](img/p2p-zaps/014.png)

---

# P2P zaps

\center{Summary:}

\center{\textbf{Lightning on the Application layer}}

---

\center{\tiny Reminder to show notifications}

---

\center{\textbf{\underline{Challenges}}}

---

# Challenges

- zaps must include forwarding fee
- wallets vs protocols

---

# Challenges

![](img/wallets-vs-protocols.png)

---

# Challenges

- share wallets between multiple devices
- encrypted send credentials vs plaintext receive credentials
- how to test send credentials?

---

# Challenges

- user education
- high availability lightning node
- liquidity issues
- forwarding to multiple receivers

\center{\textbf{What if somebody has no lightning wallet?}}

---

# Cowboy Credits

Cowboy Credits exist to smooth over UX issues:

- new users do not have a wallet
- receiving sats can fail for many reasons
- some users prefer UX over sats

\center{\textbf{CCs are non-withdrawable}}

---

# Cowboy Credits

Also:

- used first to pay SN instead of sats
- backup for lightning network issues
- 30% of a zap go to territory founders and rewards \textbf{as sats}

\center{\textbf{Half-life of a CC is two zaps}}

---

# The End

\pandocbounded{\includegraphics[width=0.4\textwidth,keepaspectratio]{img/high_on_custodial.jpg}}
\hfill
\pandocbounded{\includegraphics[width=0.4\textwidth,keepaspectratio]{img/plebpoet_thanks.png}}
