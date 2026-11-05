# Ktemia Flight Search skill for Claude Code

A Claude Code skill that searches and compares flights with the [Ktemia](https://www.ktemia.com/) [flight search API](https://www.ktemia.com/docs/api/). Ask in plain language — "find me a nonstop from New York to Paris on 10 March, back on the 17th, for two" — and the agent looks up airport codes, runs the search, and returns fares from each seller with booking links.

- **Airport lookup**: turns "Lisbon" into `LIS`, and asks when a name matches several cities
- **One-way, round trip, and multi-city** search
- **Filters**: cabin, stops, airlines, budget, passengers, market
- **Booking links**: each seller's booking page for the itinerary you pick
- **Asks instead of guessing**: no invented cities or dates, so no wasted API calls

Ktemia compares fares; it does not book tickets. The traveller books on the seller's site.

## Install

### As a Claude Code plugin

```
/plugin marketplace add Ktemiaa/ktemia-flights-skill
/plugin install ktemia@ktemia
```

### As a standalone skill

Copy `skills/flight-search` into your skills folder:

```bash
git clone https://github.com/Ktemiaa/ktemia-flights-skill.git
cp -r ktemia-flights-skill/skills/flight-search ~/.claude/skills/
```

## Set up your API key

The skill reads your key from `KTEMIA_API_KEY`:

```bash
export KTEMIA_API_KEY="your-key"
```

How to get a key, and the plan limits, are on [authentication](https://www.ktemia.com/docs/api/#authentication) and [pricing](https://www.ktemia.com/pricing/). Every API call counts as one request: a search, each results page, and each details call.

## Try it

> Find flights from Lisbon to London on 15 March 2027.

> Compare round trips from JFK to Paris, 10–17 March, two adults, at most one stop, cheapest first.

> Multi-city: Lisbon → Barcelona on 2 April, Barcelona → Rome on 6 April, Rome → Lisbon on 10 April.

## Use the client directly

The skill bundles a small Python client with no dependencies:

```bash
python3 skills/flight-search/scripts/ktemia.py airports "Lisbon"
python3 skills/flight-search/scripts/ktemia.py search --origin LIS --destination LHR --date 2027-03-15
python3 skills/flight-search/scripts/ktemia.py results <searchToken>
python3 skills/flight-search/scripts/ktemia.py details <searchToken> <flight id>
```

## Learn more

- [Flight search API reference](https://www.ktemia.com/docs/api/) — every field and error, with code in cURL, Python, Node, Go, Java, Ruby, and PHP
- [Search airports](https://www.ktemia.com/docs/api/flights/airports/) · [Search flights](https://www.ktemia.com/docs/api/flights/search/) · [List results](https://www.ktemia.com/docs/api/flights/results/) · [Flight details](https://www.ktemia.com/docs/api/flights/details/)
- [What a flight search API is, and what it is not](https://www.ktemia.com/blog/flight-search-api/)
- [Flights in Cursor and Claude: MCP, skills, and instructions](https://www.ktemia.com/blog/flights-mcp/)
- [Why there is no official Google Flights API](https://www.ktemia.com/blog/google-flights-api/)
- [Amadeus API vs Skyscanner API, after the Amadeus self-service shutdown](https://www.ktemia.com/blog/amadeus-api-vs-skyscanner-api/)
- [Kiwi Tequila API compared](https://www.ktemia.com/blog/kiwi-tequila-api/)
- [We compared 1,703 flights across 57 booking sites](https://www.ktemia.com/blog/flight-price-spread/)

## About Ktemia

[Ktemia](https://www.ktemia.com/) is a search and compare platform for flights, with stays, cars, and homes to follow. Use it in the [dashboard](https://www.ktemia.com/product/), through the [API](https://www.ktemia.com/docs/api/), or with the AI copilot. More guides are on the [blog](https://www.ktemia.com/blog/).

## License

MIT
