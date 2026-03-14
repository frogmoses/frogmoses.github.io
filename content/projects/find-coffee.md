---
title: "Finding the Right Green Coffee"
date: 2026-03-14
draft: true
tags: ["coffee-roasting", "machine-learning", "data-scraping", "flask", "similarity-search"]
---

In my [previous post about coffee roasting analysis](https://briancarroll.cool/projects/coffee-roasting/), I mentioned that I buy all my green coffee from [Sweet Maria's](https://www.sweetmarias.com) and feed their bean profiles into the analysis pipeline. What I didn't mention is how I decide what to buy in the first place.

Sweet Maria's typically has 80-100 coffees listed at any given time. Each one has cupping notes, a flavor chart with 12 scored dimensions, professional cupping scores, and a roast recommendation. That's a lot of data to compare by scrolling through a product list. I kept finding myself opening 10 tabs, reading descriptions, forgetting what the first one said, and eventually just picking something that sounded good.

So I built a tool to do it better.

find-coffee scrapes the current inventory, stores everything in a local SQLite database, and gives me a simple web UI to search and compare coffees. The interesting part is the similarity search. I wanted to be able to click on a coffee I liked and ask "what else is like this?"

I implemented three approaches because it turns out "similar" means different things depending on what you care about.

The first is text-based. Cupping notes are free-text descriptions like "bittersweet chocolate, dried cherry, brown sugar, hints of jasmine." I tokenize and stem these with NLTK, build TF-IDF vectors with scikit-learn, and compute cosine similarity. This finds coffees that are *described* in similar language.

The second is flavor profile-based. Each coffee has 12 scored dimensions — floral, honey, sugar, caramel, fruit, citrus, berry, cocoa, nut, rustic, spice, and body — all integers from 0 to 10. I treat these as a 12-dimensional vector and compute cosine similarity directly. This finds coffees that have a similar *structure*, even if they're described differently.

The third is a weighted average of both. In practice this gives the most useful results because it catches coffees that are similar in both how they're described and how they're scored.

Each returns the top 3 matches. The UI has buttons for all three so I can compare perspectives quickly.

One design decision I'm happy with is the two-table schema. The scraped inventory is ephemeral — it resets every time I scrape because coffees come and go as they sell out. But when I click a coffee name to buy it, the app snapshots all of its data into a permanent purchases table. Months later I can still see the full flavor profile and cupping notes of everything I've bought, even though most of those coffees are long gone from the site.

That purchase table is also what bridges into the roasting side. I can query it by origin or name when planning what to roast next, and the bean profile data feeds into the [roasting analysis pipeline](https://briancarroll.cool/projects/coffee-roasting/).

The whole thing is Flask + SQLAlchemy with a Click CLI, running locally. No cloud, no auth, just a SQLite file on my laptop. The ML is straight-forward — TF-IDF and cosine similarity.

This is one of the tools I mentioned at the end of the roasting post. The ecosystem now looks like: find-coffee handles sourcing, [r1-eye](https://briancarroll.cool/projects/r1-eye/) and [gopro-eye](https://briancarroll.cool/projects/gopro-eye/) handle visual monitoring during the roast, and the [roasting analysis pipeline](https://briancarroll.cool/projects/coffee-roasting/) ties it all together with recommendations for the next batch.

I'm not releasing this one publicly since it's a scraper pointed at someone else's website. But the approach is straightforward enough to adapt to any domain where you have structured + unstructured data and want to find "more like this."
