---
cssclasses: literature-note
tags:
  - {{itemType}}
aliases:
  - "{{title}}"
title: "{{title}}"
shortTitle: "{%- if creators and creators[0] -%}{{creators[0].lastName if creators[0].lastName else creators[0].name}}{%- if date %} ({{date | format('YYYY')}}){%- endif -%}{%- else -%}{{title}}{%- endif -%}"
authors:
{%- for type, creators in creators | groupby("creatorType") %}{%- for creator in creators %}
  - "{%- if creator.name %}{{creator.name}}{%- else %}{{creator.lastName}}, {{creator.firstName}}{%- endif %}"
{%- endfor %}{%- endfor %}
year: {{date | format("YYYY")}}
citekey: "{{citekey}}"
{% if itemType -%}
itemType: "{{itemType}}"
{%- endif %}
{% if itemType == "journalArticle" -%}
journal: "{{publicationTitle}}"
{%- endif %}
{% if volume -%}
volume: "{{volume}}"
{%- endif %}
{% if issue -%}
issue: "{{issue}}"
{%- endif %}
{% if itemType == "bookSection" -%}
book: "{{publicationTitle}}"
{%- endif %}
{% if publisher -%}
publisher: "{{publisher}}"
{%- endif %}
{% if place -%}
location: "{{place}}"
{%- endif %}
{% if pages -%}
pages: "{{pages}}"
{%- endif %}
{% if DOI -%}
doi: "{{DOI}}"
{%- endif %}
{% if ISBN -%}
isbn: "{{ISBN}}"
cover: "https://covers.openlibrary.org/b/isbn/{{ISBN}}-L.jpg"
{%- endif %}
{% if url -%}
url: "{{url}}"
{%- endif %}
rating:
status: unread
contribution:
pdfLink: "{{ pdfZoteroLink | default("") | replace(r/^\[.*\]\(|\)$/g, "") }}"
imported: "{{importDate | format("DD-MM-YYYY h:mm a")}}"
---
## {{title}}

{% if ISBN %}
<div class="book-cover-container">
  <img src="https://covers.openlibrary.org/b/isbn/{{ISBN}}-L.jpg" alt="Cover: {{title}}{%- if creators[0] %} von {{creators[0].lastName if creators[0].lastName else creators[0].name}}{%- endif %}" class="book-cover" loading="lazy" />
</div>

{% endif %}

> [!book] Quelle
> {{bibliography}}

{%- if abstractNote %}

> [!abstract] Kurzfassung
> {{abstractNote}}
{% endif %}

## Meine Notizen

{% for annotation in annotations -%}

{# Text Highlights #}
{%- if annotation.annotatedText -%}
<div class="annotation-highlight">
  <span class="section-marker"></span>
  <mark class="hltr-{{annotation.colorCategory | lower | default('yellow')}}">"{{annotation.annotatedText | safe}}"</mark>
  {%- if itemType == "book" and annotation.page %} <span class="annotation-page">(S. {{annotation.page}})</span>{%- endif %}
</div>
{%- endif -%}

{# Bilder (Screenshots) - Wikilink direkt, Caption danach #}
{%- if annotation.imageRelativePath -%}

![[{{ annotation.imageRelativePath | replace(r/^.*\//g, "") }}]]

<div class="annotation-figure-caption">
  <span class="figure-label"></span>
  {%- if annotation.page %}<span class="figure-source">Seite {{annotation.page}}</span>{%- endif %}
</div>
{%- endif -%}

{# Kommentar immer zuletzt (unter Highlight oder Bild) #}
{%- if annotation.comment %}

<div class="annotation-comment">
  <span class="comment-label">Anm.:</span> {{annotation.comment}}
</div>
{%- endif %}


{% endfor %}