# bandwagonhost speed test: how to check latency, bandwidth and routes in every data center before you spend a dollar

Searching for a "bandwagonhost speed test" usually means one thing: you're about to buy a VPS from BandwagonHost (搬瓦工) and you want proof of how fast each data center actually is from your network — not marketing claims. The good news is you don't need to buy anything first. BandwagonHost publishes a test IP for nearly every data center, hosts 100MB download files, and runs public demo sites with built-in SpeedTest and LookingGlass tools. Three free checks, about ten minutes, and you'll know which machine room fits your line.

> **Quick pick:** for most readers testing from mainland China, the plan that makes sense is the CN2 GIA-E entry plan — 2.5 Gbps port, 1 TB monthly traffic, 12 switchable data centers, **$49.99/quarter or $169.99/year**. It rides the same CN2 GIA routes you're about to test at DC6 and DC9. 👉 [check current CN2 GIA-E pricing and availability](https://bit.ly/BandwaGon)

## Three ways to run a speed test before buying

The standard method combines ping, a real download, and a route trace. Each answers a different question: ping shows raw latency, the download shows usable bandwidth, and LookingGlass shows which backbone your traffic actually rides.

**1. Ping the test IPs.** Every major BandwagonHost data center has a public test IP. Ping it from your own connection, and the `time=` value is your latency in milliseconds. If you want a country-wide picture instead of just your own line, multi-location ping tools like chinaz's ping service show results from dozens of Chinese nodes at once.

| Data center | Location | Test IP |
| --- | --- | --- |
| HK85 | Hong Kong | 45.78.18.149 |
| HK CN2 GIA | Hong Kong | 93.179.124.115 |
| JPOS_1 | Osaka (SoftBank) | 185.212.59.222 |
| DC39 | Tokyo | 74.82.192.227 |
| USCA_6 (DC6) | Los Angeles, CN2 GIA-E | 162.244.241.102 |
| USCA_9 (DC9) | Los Angeles, CN2 GIA | 65.49.131.102 |
| USCA_3 (DC3) | Los Angeles, CN2 | 23.252.103.101 |
| USCA_4 (DC4) | Los Angeles, MCOM | 98.142.136.11 |
| USNY_2 | New York | 208.167.227.122 |
| USNJ | New Jersey | 23.29.138.5 |

One caveat: the same data center can have several test IPs floating around in community guides (DC6, DC8 and DC9 each appear with two different addresses in different lists). If one IP looks odd, ping another one for the same location before drawing conclusions.

**2. Download a test file.** Ping tells you latency, not throughput. Several data centers host a 100MB file you can pull with a browser or `wget` to see real sustained speed — for example `http://23.252.96.201/100mb.bin` at DC2, `http://98.142.136.11/100mb.bin` at DC4, and `http://208.167.227.122/100mb.bin` in New York. A plan with a 2.5 Gbps port means nothing if your route throttles you to 2 MB/s at 9 p.m., so test at the hour you'll actually use the VPS.

**3. Open a LookingGlass demo site.** The demo sites for DC6 (`dc6.bwg.net`), DC9 (`dc9.bwg.net`), Osaka SoftBank (`jpos.bwg.net`) and New York (`usny.bwg.net`) include an online SpeedTest plus Ping/MTR/Traceroute tools. The traceroute is the part most guides skip: it's how you verify a plan actually routes through CN2 GIA (AS4809) rather than the congested CN2 GT network — two route tiers that feel completely different at peak hours despite similar names.

## What the numbers should look like

Latency from mainland China falls into clear bands depending on location and route:

| Data center / route | Typical latency from China |
| --- | --- |
| Hong Kong CN2 GIA | 30–50 ms |
| Tokyo CN2 GIA | 60–90 ms |
| Osaka SoftBank | 70–100 ms |
| Los Angeles DC6 / DC9 (CN2 GIA) | 150–180 ms |
| Los Angeles DC3 (CN2 GT) | 160–200 ms |
| New York / New Jersey / Europe | 200 ms+ |

DC9 has been measured per-carrier, and the spread is worth knowing: China Telecom averages around 158 ms (Shanghai as fast as 131 ms), China Mobile around 174 ms, and China Unicom around 192 ms. On a well-routed CN2 GIA line, community tests report near-zero packet loss at peak hours — that stability is the entire reason people pay the CN2 premium. One recent one-command test script covering 13 data centers produced a similar picture from its vantage point: Los Angeles locations in the 155–166 ms range, Fremont at 172 ms, while New Jersey (238 ms) and New York (245 ms) landed in "fair" territory.

A rough rule of thumb after your tests: under ~180 ms to a Los Angeles CN2 GIA IP with low jitter means the route is healthy for you. If your ping to DC6/DC9 comes back at 250 ms+ while the LookingGlass shows clean routing from elsewhere, the problem is your local line or transit, and an Asia-Pacific machine room (Hong Kong or Japan) is the better match.

## Matching your test results to a plan

BandwagonHost's currently listed plans on its own order page split into two families. All are KVM with RAID-10 SSD, free automatic backups and snapshots, 1 dedicated IPv4, a routed /64 IPv6 subnet, full root access, and instant rDNS control; 160G plans and up add a secondary private network interface.

**Standard KVM PROMO plans** (multiple US locations plus Canada/Europe, free migration between eligible data centers):

| Plan | RAM / SSD / Traffic | Port | Price (USD) | Buy |
| --- | --- | --- | --- | --- |
| 20G KVM PROMO | 1 GB / 20 GB / 1 TB/mo | 1 Gbps | $49.99/yr | [ Buy 20G KVM](https://bit.ly/BandwaGon) |
| 40G KVM PROMO | 2 GB / 40 GB / 2 TB/mo | 1 Gbps | $52.99/6mo · $99.99/yr | [ Buy 40G KVM](https://bit.ly/BandwaGon) |
| 80G KVM PROMO | 4 GB / 80 GB / 3 TB/mo | 1 Gbps | $19.99/mo · $59.99/qtr · $199.99/yr | [ Buy 80G KVM](https://bit.ly/BandwaGon) |
| 160G KVM PROMO | 8 GB / 160 GB / 4 TB/mo | 1 Gbps | $39.99/mo · $112.99/qtr · $399.99/yr | [ Buy 160G KVM](https://bit.ly/BandwaGon) |
| 320G KVM PROMO | 16 GB / 320 GB / 5 TB/mo | 1 Gbps | $79.99/mo · $227.99/qtr · $799.99/yr | [ Buy 320G KVM](https://bit.ly/BandwaGon) |
| 480G KVM PROMO | 24 GB / 480 GB / 6 TB/mo | 1 Gbps | $119.99/mo · $341.99/qtr · $1199.99/yr | [ Buy 480G KVM](https://bit.ly/BandwaGon) |

**Singapore CN2 GIA plans** (Singapore Equinix SG1, 1.5–5 Gbps ports):

| Plan | RAM / SSD / Traffic | Port | Price (USD) | Buy |
| --- | --- | --- | --- | --- |
| SG 40G | 2 GB / 40 GB / 500 GB/mo | 1.5 Gbps | $49.99/mo · $139.99/qtr · $499.99/yr | [ Buy SG 40G](https://bit.ly/BandwaGon) |
| SG 80G | 4 GB / 80 GB / 1 TB/mo | 1.5 Gbps | $86.99/mo · $245.99/qtr · $869.99/yr | [ Buy SG 80G](https://bit.ly/BandwaGon) |
| SG 160G | 8 GB / 160 GB / 2 TB/mo | 2.5 Gbps | $165.99/mo · $479.99/qtr · $1665.99/yr | [ Buy SG 160G](https://bit.ly/BandwaGon) |
| SG 320G | 16 GB / 320 GB / 4 TB/mo | 2.5 Gbps | $329.99/mo · $929.99/qtr · $3199/yr | [ Buy SG 320G](https://bit.ly/BandwaGon) |
| SG 640G | 32 GB / 640 GB / 6 TB/mo | 5 Gbps | $549.99/mo · $1569.99/qtr · $5549.99/yr | [ Buy SG 640G](https://bit.ly/BandwaGon) |
| SG 1280G | 64 GB / 1280 GB / 8 TB/mo | 5 Gbps | $1059.99/mo · $2999.99/qtr · $10559.99/yr | [ Buy SG 1280G](https://bit.ly/BandwaGon) |

The plan most speed-test-driven buyers actually land on is the Los Angeles CN2 GIA-E (E-Commerce) line, which appears across multiple independent guides rather than the main order page: the entry tier carries 2 cores, 1 GB RAM, 20 GB SSD, 1 TB of monthly traffic on a 2.5 Gbps port for **$49.99/quarter or $169.99/year** (no monthly billing), with free migration across 12 data centers including DC6, DC9 and Osaka SoftBank. A higher-traffic 2 GB/2 TB version runs about $89.99/quarter or $299.99/year. BandwagonHost's own guidance, as quoted in community writeups, is blunt: if latency isn't the deciding factor, take the Los Angeles E-Commerce plan — which is exactly what your speed test is there to determine. Hong Kong CN2 GIA plans (2 GB+/500 GB at $89.99/month, or a 4 GB+/1 TB big-bandwidth tier at $155.99/month) sit in the premium tier: lowest latency to China, highest price.

If your ping results put Hong Kong or Tokyo in the 30–90 ms band and that's what your use case needs (game servers, latency-sensitive remote desktop), the premium tier is justified. For websites, proxies, and most SSH work, 150–180 ms Los Angeles CN2 GIA is comfortably usable and costs a fraction as much. 👉 [see all current plans and data center options](https://bit.ly/BandwaGon)

## The cost math most reviews skip

Two billing details change the real price of that CN2 GIA-E plan, and neither is obvious from a spec sheet.

**Quarterly looks cheap but isn't.** Four quarters of the CN2 GIA-E entry plan cost $199.96; the annual term is $169.99. Paying yearly saves roughly $30 (about 15%) and locks the rate. The smarter play for a first purchase: start with one quarter at $49.99 as a paid trial, run your own speed tests at peak hours for a couple of months, then switch to annual once you're satisfied. There's also a **30-day money-back guarantee** on first purchases, so the initial risk window is short either way.

**The recurring promo code works on renewals.** The code `BWHCGLUKKB` takes 6.77% off at checkout and, per multiple guides, keeps applying at every renewal — not just the first invoice. On the $169.99 annual CN2 GIA-E plan that brings the first year to roughly $158.50. Apply it in the promo field during checkout and confirm the discount shows before paying. Payment methods include Alipay, UnionPay, PayPal and credit cards.

## Restrictions that only surface after purchase

A few limits live in the terms and panel rather than the pricing page, and two of them intersect directly with the speed-testing theme:

- **Blocked IPs cost $8 to replace.** BandwagonHost no longer replaces IPs for free. You can alternatively migrate to another data center to get a fresh IP at no charge — but migration is locked while the IP is blacklisted, so you'd need to unblock first or contact support. If your speed test shows high packet loss to your own VPS later, run the blacklist check from the KiwiVM control panel (the "Test Main IP" function) before blaming the route; "IP NOT BLOCKED" means the slowdown is elsewhere.
- **Migration changes your traffic economics.** Standard KVM plans migrate freely between eligible data centers, but moving one to a CN2 machine room cuts your monthly traffic allowance to one-third. A 1 TB/mo plan becomes ~333 GB after that move.
- **Everything is self-managed.** BandwagonHost keeps prices low by not offering managed support. If you need someone to configure your stack for you, this is the wrong shop.
- **Limited Edition flash plans are non-migratable.** Occasional $19–49.99/year promo plans appear and sell out fast, but they can't be moved between data centers — fine if you've already tested that specific location, a trap if you haven't.

## FAQ

**Do I need to buy a VPS to test the speed?** No. Test IPs, 100MB download files and LookingGlass demo sites are all public. Buying first is only necessary to test from inside the VPS (an iperf or SpeedTest CLI run), which is a reasonable second step after the pre-purchase checks.

**Which data center should I pick for China access?** Whichever your tests favor. Hong Kong CN2 GIA tests lowest (30–50 ms), Tokyo and Osaka land in the 60–100 ms band, and Los Angeles DC6/DC9 sit around 150–180 ms with the most stable peak-hour routing per community measurements. DC6 has more exit-bandwidth headroom and connects directly into Los Angeles local internet; DC9's outbound traffic transits China Telecom's network. CN2 GIA-E plans can switch between them at will, so you don't have to guess perfectly.

**What if my ping is fine but the download is slow?** That usually means route congestion at peak hours or a throttled intermediate link rather than a blocked IP. Re-test at a different time of day and compare the LookingGlass traceroute — if the path detours through congested transit networks instead of AS4809, the route tier is the problem.

**Can I change data centers after buying?** Yes, on migratable plans, free of charge, from the KiwiVM panel — with the blocked-IP and traffic-division caveats above.

## Before you click buy

Match your test results to your budget: only the cheapest KVM tier needed and latency irrelevant → the $49.99/year 20G KVM plan. China-facing traffic where stability matters → CN2 GIA-E at $169.99/year (or one $49.99 quarter as a trial first). Latency under 100 ms genuinely required → Hong Kong CN2 GIA at $89.99/month, and accept the price. Whatever you choose, run the peak-hour test before the annual upgrade, and apply `BWHCGLUKKB` at checkout. 👉 [start with the CN2 GIA-E quarterly plan at $49.99](https://bit.ly/BandwaGon)
