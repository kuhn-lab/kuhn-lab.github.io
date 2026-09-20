---
layout: single
title: Publications
permalink: /publications/
---

## 📚 Lab publications

{% assign sorted_pubs = site.publications | sort: 'year' | reverse %}
{% for pub in sorted_pubs %}
### {{ pub.title }}
- **Authors:** {{ pub.authors }}
- **Journal:** {{ pub.journal }} ({{ pub.year }})
- {% if pub.doi and pub.doi != "" %}[DOI Link](https://doi.org/{{ pub.doi }}){% endif %}
- {{ pub.content | markdownify }}

---
{% endfor %}
