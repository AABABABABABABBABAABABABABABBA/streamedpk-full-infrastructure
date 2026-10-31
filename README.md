
-- Streamed.pk has since then stopped operating ( nothing is removed from when I first made this )


# streamed.pk full infrastructure (2026-10-17

# A. Domains & registrars

# Domain Role Registrar Created DNS streamed.pk main site



# PKNIC (.pk, $15.99/yr, biennial)



# 2025-04-30



# jason/penny.ns.cloudflare.com



# official mirror

# streamed.st

# IncogNET

# 2025-04-29

# vasilii/zoe.ns.cloudflare.com

# embed.st

# video embed player

# ns.isp.{st,gd,vg,fo}

# strmd.st

# video LB/CDN parent







# strmd.link + status.strmd.link



# mirror list + status page

# Cloudflare

# cdn-lab.shop (a.cdn-lab.shop)

# analytics + ads

# brodie/kia.ns.cloudflare.com

# movy.bz -> movy.sx

# related/redirect site

# Netim SARL (.sx)

# rocco/carla.ns.cloudflare.com





# ppv.st



# paid subscription (current)



# IncogNET (.st, $17.76/yr)



# 2025-10-23



# boyd/olga.ns.cloudflare.com





# ppv.to



# legacy / parked “seized”



# Tonic (.to, $50/yr)



# 2025-06-12



# ns1/ns2.seizedservers.com (no HTTPS at check)

# B. Edge / network layer







# Asset IP Network
# Location

# streamed.pk / streamed.st



# 190.115.31.74 / .224



# AS59692 IQWeb FZ-LLC



# Belize City, BZ



# server: ddos-guard, rDNS ddos-guard.net; origin hidden





# ppv.st / api.ppv.st



# 190.115.31.207



# AS59692 IQWeb FZ-LLC



# Belize City, BZ



# same edge pattern as streamed; Nuxt SPA





# embed.st (player)



# 81.17.16.194



# AS51852 Private Layer INC



# Bellinzona, CH



# hostedby.privatelayer.com





# lb1.strmd.st



# 92.63.196.207



# AS202425 IP Volume inc



# Amsterdam, NL


# plain nginx

# lb2.strmd.st

# 92.63.196.206

# AS202425 IP Volume inc

# Amsterdam, NL

# serves playlist + segments

# lb3.strmd.st

# 92.63.196.205

# AS202425 IP Volume inc

# Amsterdam, NL

# plain nginx





# lb4.strmd.st



# 92.63.196.204



# AS202425 IP Volume inc



# Amsterdam, NL



# plain nginx
 
# P2P/cache: SwarmCloud @swarmcloud/hls (WebRTC), JW Player 8.38.10 + lock.wasm served from BunnyCDN pull zone 6181792 (strmd.b-cdn.net; origin likely GCS - inferred).

# C. Public API (no auth required, documented at /docs)

# Match endpoints:





# GET /api/matches/all , /api/matches/all/popular

# GET /api/matches/all-today , /api/matches/all-today/popular

# GET /api/matches/live , /api/matches/live/popular , /api/matches/live/popular-viewcount

# GET /api/matches/featured

# GET /api/matches/[SPORT] , /api/matches/[SPORT]/popular

# Stream endpoints (source codenames documented):

# GET /api/stream/{alpha|bravo|charlie|delta|echo|foxtrot|golf|hotel|intel}/{id}
# -> [{id, streamNo, language, hd, embedUrl, source, viewers}]

# Observed live sources: hotel, golf, admin (+ documented alpha..intel)

# embedUrl pattern: https://embed.st/embed/{source}/{id}/{streamNo}

# Other:

# GET /api/sports  (15 categories: basketball, football, american-football, hockey, baseball,
# motor-sports, fight, tennis, rugby, golf, billiards, afl, darts, cricket, other)



# GET /api/images/badge/[id].webp



# GET /api/images/poster/[badge]/[badge].webp



# GET /api/images/proxy/[poster].webp



# POST /api/feedback   (GET returns 405)



# Rate limits: none stated

# D. Video pipeline





# SPA -> GET /api/matches/live/popular (needs DDoS-Guard cookie _ddg1...)



# -> GET /api/stream/{source}/{id} -> embedUrl on embed.st



# embed.st loads Clappr + SwarmCloud P2P (jsDelivr) + JW Player (BunnyCDN)



# Playlist: https://lb{n}.strmd.st/secure/{token}/{source}/stream/{id}/{n}/playlist.m3u8

# header "## Processed by GOAT", 6s segments, tokenized /b/{shard}/m/{long-token}.ts paths

# Anti-scrape: direct curl of a segment -> 403; non-player fetch -> image/webp decoy (not verified as real media)

# E. Support / ops surface

# Status page: status.strmd.link -> Main / API / Embed / CDN (Provider Host); "Official Streamed Mirror List"

3 Mirror list page: strmd.link -> lists streamed.pk + streamed.st ("Online")

# Self-hosted Plausible analytics (obfuscated as a.cdn-lab.shop/js/script.js, POSTs to /api/event)

# Related site movy.sx / movy.bz: Next.js front (x-nextjs-cache), backend.movy.sx, fy.movy.sx (Express,
# x-powered-by: Express, CSP default-src 'none'), all behind Cloudflare

# ppv.st: current paid subscription / PPV front (linked from streamed SPA); api.ppv.st serves stream metadata; DDoS-Guard + Cloudflare DNS

# ppv.to: old .to brand; NS points at seizedservers.com and HTTPS did not respond — treat as retired or a staged seizure page, not the live product (unless the app still hardcodes .to links)

# F. Cost model inputs (2026-10-17)

# FX: 1 USD = 1.414 CAD ; 1 USD = 83.6 RUB


# BunnyCDN: volume $0.005/GB (0-500TB) => $5/TB ; standard EU/NA $0.01/GB, Asia $0.03, SA $0.045, MEA $0.06

# DDoS-Guard RU website tiers/mo: 8k / 20k / 48k / 80k / 200k RUB => ~$96 / 241 / 578 / 963 / 2407
# => ~C$136 / 341 / 817 / 1362 / 3404

# DDoS-Guard network L3-4 "Basic" always-on: $350/mo (~C$495)

# Private Layer: VM from $59/mo, dedicated from $119/mo, up to ~$4,999/mo

# Domains: .pk $15.99/yr, .st $17.76/yr, .to $50/yr

# Bandwidth: 1,000 viewers @2.5Mbps = 1.125 TB/hour
