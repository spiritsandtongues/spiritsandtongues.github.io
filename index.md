---
layout: default
title: Spirits and Tongues
---

# Spirits and Tongues

## Episodes

{% assign episodes = site.episodes | sort: "number" | reverse %}
{% for episode in episodes %}
### [{{episode.number}} - {{episode.title}}]({{episode.url}})

{{episode.content}}
{% endfor %}