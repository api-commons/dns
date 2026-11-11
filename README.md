# DNS and Domains

The common DNS vocabulary -- the domains people register, the zones that serve them and the records inside those zones -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged DNS, Domains, Domain Registration, Domain Names, Registrar, Domain Management, Hosting in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| domain | 23 | 20 | id 70%, name 70%, created_at 55% | domains 21, domain 4, registrations 2 |
| zone | 7 | 7 | id 86%, name 86%, created_at 71%, status 57% | zones 5, zone 2 |
| dns_record | 18 | 15 | name 100%, type 100%, ttl 93%, id 67%, priority 67% | records 14, rrsets 2, rrset 1, dns_records 1 |

Cohort: 69 providers with harvested OpenAPI, 28 crosswalks. Of the providers exposing a domain: 70% create, 87% list, 70% fetch, 52% update, 52% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A DNS record agrees on name, type, TTL, priority and id across registrars, DNS hosts and clouds (Cloudflare, Route 53, Google Cloud DNS, Hetzner) -- the record is fixed by the DNS protocol, and the APIs follow it. Its content is the one field named differently everywhere (content, value, rdata, rrdatas, target).
- A domain agrees on name, id and created_at; expiry, auto-renew and nameservers are each carried by too few registrars to share.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Records, resource-record sets and DNS records are one concept, published beneath their zone at `/zones/{zone_id}/records`.
- Zones count only at a provider that also exposes records; hosted zones and managed zones are zones.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
