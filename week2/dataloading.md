---
title: Data Loading
parent: Woche 2
nav_order: 4
previous: Session Storage
---

BEschreibung!!!....

{% assign t1-header = "Task" %}
{% assign t1-question = "Schreiben Sie einen Hook, der sich um das Laden der Transaktions Daten und der Account Details kümmert. Achten Sie darauf, dass Datenabfragen ein gültiges Token benötigen." %}
{% capture t1-hint %}

<ul>
<li>Machen Sie Gebrauch vom useEffect Hook und Dependencies List. </li>
<li>Schreiben Sie individuelle Hooks für Account und Transaktionen. </li>
<li>Die benötigten API Funktionen sind bereits implementiert.</li>
</ul>
{% endcapture %}
{% include task.html header=t1-header task=t1-question  hint=t1-hint %}



{% assign s-header = "Solution" %}
{% assign s-solution = "https://gitlab.ost.ch/etienne.baumgartner/bor_final/-/compare/session_storage_solution...data_loading_solution?from_project_id=4572" %}
{% include solution.html solution=s-solution %}