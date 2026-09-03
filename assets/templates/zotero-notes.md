---
title: "{% if caseName %}{{caseName | escape}}{% elif nameOfAct %}{{nameOfAct | escape}}{% else %}{{title | escape}}{% endif %}"
author: {% if court %}{{court}}{% else %}{{authors}}{% endif %}
year: {{date | format("YYYY")}}
type: {{itemType}}
citekey: {{citationKey}}
collection: {{collections[0].name}} 
tags: [{% if allTags %}{{allTags}}{% endif %}]
created: 2025-07-14
modified: 2026-08-22
---

{{bibliography | replace("1.", "")}}

{{pdfZoteroLink}}

## Notes

{% persist "notes" %}{% if isFirstImport %}
*Notes written here will persist after updates.* 
{% endif %}
{% endpersist %}

## In-text annotations

{% for annotation in annotations -%}
{%if annotation.annotatedText -%}
{% if annotation.color %} <mark class="hltr-{{annotation.colorCategory | lower}}">{{annotation.annotatedText | safe}}</mark> {% else %} {{annotation.type | capitalize}} {% endif %} ([Page {{annotation.pageLabel}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}})) {%endif %}

{% if annotation.comment %} <mark class="hltr-{{annotation.colorCategory | lower}}">{{annotation.comment | safe}}</mark> ([Page {{annotation.pageLabel}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}})) {% endif %}

{%if annotation.imageRelativePath %} 
![[{{annotation.imageRelativePath}}]]
{%endif %}
{% if annotation.allTags %}
{{annotation.allTags}}
{% endif %}
{% endfor -%}
