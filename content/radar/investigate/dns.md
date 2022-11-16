---
pcx_content_type: reference
title: DNS
weight: 2
---

# DNS

Access aggregated and anonymized DNS queries to Cloudflare's [1.1.1.1](/1.1.1.1//) public resolver service.

## List of endpoints

### Top locations

#### Example: Geographical distribution of `google.com` versus `yandex.ru`

In the next example, we will request the top originating locations for `google.com` DNS queries:

```bash
curl -X GET "https://api.cloudflare.com/client/v4/radar/dns/top/locations?domain=google.com&dateRange=1d&format=json&limit=2" \
     -H "Authorization: Bearer <API_TOKEN>"
```

The response shows that most queries come from the United States and Brazil:

```json
{
  "clientCountryAlpha2": "US",
  "clientCountryName": "United States",
  "value": "43.474518"
}, {
  "clientCountryAlpha2": "BR",
  "clientCountryName": "Brazil",
  "value": "10.772799"
}
```

Making the same search request for `yandex.ru`, a Russian search engine:

```bash
curl -X GET "https://api.cloudflare.com/client/v4/radar/dns/top/locations?domain=yandex.ru&dateRange=1d&format=json&limit=2" \
     -H "Authorization: Bearer <API_TOKEN>" \
     -H "Content-Type: application/json"
```

Returns the following response:

Returns the following response:

```json
{
  "clientCountryAlpha2": "RU",
  "clientCountryName": "Russian Federation",
  "value": "73.710495"
}, {
  "clientCountryAlpha2": "DE",
  "clientCountryName": "Germany",
  "value": "5.518052"
}
```

As expected, most queries come from Russia.

{{<Aside type="note">}}
Note that these examples return the total number of DNS queries from a location to a hostname, _out_ of the total DNS queries to a given hostname. In this sense, it is expected that locations with higher population numbers — like the United States — frequently appear in the top spots, even if the actual percentage is low.
{{</Aside>}}

You can also provide multiple hostnames. Refer to [Get top locations by DNS queries](https://developers.cloudflare.com/api/operations/radar-dns-get-top-locations-by-dns-queries) for more information. This is useful when the application you want to explore uses several hostnames to serve its content (like a hostname for the main website, another hostname dedicated to its API, etc.).

## Next steps

Refer to [Domain ranking](/radar/investigate/domain-ranking-datasets/) for more information on rankings generated by Cloudflare based on DNS queries to [1.1.1.1 public resolver](/1.1.1.1/).