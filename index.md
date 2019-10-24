---
layout: default
title: Spirits and Tongues
---

# Spirits & Tongues

<img class="logo" src="./images/logo.png">

<div class="subtitle">an incomplete list of my obsessions</div>

---

## Episodes

{% assign episodes = site.episodes | sort: "number" | reverse %}
{% for episode in episodes %}
<div class="episode">
<h3>Episode {{episode.number}}: {{episode.title}}</h3>

{% capture episode-id %}
{{episode.episodeId}}
{% endcapture %}
{% include audio-player.html id=episode-id %}

{{episode.content}}
</div>
{% endfor %}