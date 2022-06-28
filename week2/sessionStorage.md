---
title: Session Storage
parent: Woche 2
nav_order: 3
previous: Conditional Rendering
---

# Session Storage

Der [Session Storage](https://www.w3schools.com/jsref/prop_win_sessionstorage.asp) wird gebraucht, um Daten als Key/Value im Browser abzulegen. Die naheligenste Anwendung ist das Ablegen eines Users, um das wiederholte Anmelden bei einem Refresh zu umgehen.

Dabei ist zu beachten, dass es sich die Lebenszeit der Daten im **Session** Storage auf eine Session beschränken. Wird ein Fenster/Tab geschlossen, das den Session Storage benützt, gehen ebenfalls alle Daten im Session Storage verloren.

Für eine längere Lebenszeit siehe [Local Sotage](https://www.w3schools.com/jsref/prop_win_localstorage.asp).

Für die BOR Anwendung sollen Sie den Session Storage einrichten. Dies verhindert die erzwungene Neuanmeldung nach einem Page Refresch (kommt in der Entwicklung sehr oft vor).

{% assign q1-header = "Quiz" %}
{% assign q1-question = "Welche Daten sollen im Session Storage abgelegt werden?" %}
{% capture q1-answer %}
`User` und `Token`.
{% endcapture %}
{% include quiz.html header=q1-header question=q1-question answer=q1-answer %}

{% assign q2-header = "Quiz" %}
{% assign q2-question = "In welcher Funktion soll der Session Storage eingesetzt werden?" %}
{% capture q2-answer %}
Direkt in der `authenicate` Funktion.
{% endcapture %}
{% include quiz.html header=q2-header question=q2-question answer=q2-answer %}

{% assign t1-header = "Task" %}
{% assign t1-question = "Fügen Sie die benötigten Daten in den Session Storage ein." %}
{% capture t1-hint %}

<ul>
<li>Achten Sie darauf, die bisherige Funktionalität der State Objekte (User, Token, isAuthenticated) sicherzustellen.</li>
<li>Der initiale State eines Objekts kann direkt mit den Daten des Session Storages initiiert werden. </li>
<li>isAuthenticated muss bei Änderungen von User und Token geändert werden.</li>
<li>Benutze JSON.stringify und JSON.parse für den User</li>
</ul>
{% endcapture %}
{% include task.html header=t1-header task=t1-question  hint=t1-hint %}

{% assign s-header = "Solution" %}
{% assign s-solution = "https://gitlab.ost.ch/etienne.baumgartner/bor_final/-/compare/conditional_rendering_solution...session_storage_solution?from_project_id=4572" %}
{% include solution.html solution=s-solution %}
