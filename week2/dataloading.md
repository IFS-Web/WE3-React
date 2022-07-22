---
title: Data Loading
parent: Woche 2
nav_order: 4
previous: Session Storage
---

# Data Loading

Mit der Implementation der Login Funktionalität können wir uns nun mit dem Fetching der Daten auseinandersetzen.

In der BOR Anwendung sollen die Daten nach der Weiterleitung von der Login auf die Dashboard Page gefetched und im State der Komponenten abgelegt werden.

Die GET Funktion der User Details und den assozierten Transaktionen sind im `api.js` File bereits implementiert.

## api.js

Einer der Funktionen, die Sie im Verlaufe dieser Übung verwenden werden ist `getAccountDetails`.

```jsx
export function getAccountDetails(token) {
  return getAuthenticatedJson(`/accounts`, token).then(parseJSON);
}
```

{% assign q1-header = "Quiz" %}
{% assign q1-question = "Lesen Sie die Implementation von `getAuthenticatedJson` und erklären Sie den Nutzen dieser Funktion." %}
{% capture q1-answer %}
Die Funktion erweitert den Header eines GET Request mit dem vom Login erhaltenen JWT und ermöglicht somit die Authorisierung auf die Resourcen des Backends.

```jsx
function getAuthenticatedJson(endpoint, token) {
  return fetch(`${backend}${endpoint}`, {
    method: "GET",
    headers: {
      Authorization: `Bearer ${token}`,
      Accept: "application/json",
    },
  }).then(checkStatus);
}
```

{% endcapture %}
{% include quiz.html header=q1-header question=q1-question answer=q1-answer %}

{% assign t1-header = "Task" %}
{% assign t1-question = "Schreiben Sie zwei Hooks, die sich um das Laden der Transaktions Daten und der Account Details kümmern. Achten Sie darauf, dass Datenabfragen ein gültiges Token benötigen." %}
{% capture t1-hint %}

<ul>
<li>Machen Sie Gebrauch vom useEffect Hook und Dependencies List. </li>
<li>Schreiben Sie individuelle Hooks für Account und Transaktionen. </li>
<li>Überlegen Sie sich eine Möglichkeit um ungewollte, wiederholte Fetches zu verhindern.</li>
<li>Die benötigten API Funktionen sind bereits implementiert.</li>
</ul>
{% endcapture %}
{% include task.html header=t1-header task=t1-question  hint=t1-hint %}

{% assign s-header = "Solution" %}
{% assign s-solution = "https://gitlab.ost.ch/etienne.baumgartner/bor_final/-/compare/session_storage_solution...data_loading_solution?from_project_id=4572" %}
{% include solution.html solution=s-solution %}

{% assign q1-header = "Quiz" %}
{% assign q1-question = "Weshalb werden hier zwei useEffect Hooks verwendet anstelle von einem?" %}
{% capture q1-answer %}

`useEffect` führt das Lambda jedes Mal aus, wenn sich abhängige Daten im Array ändern. Wenn nur ein `useEffect` verwendet wird, dann kann es sein, dass der Effekt nochmals ausgeführt wird wenn die ersten Daten geladen wurden:

```jsx
useEffect(() => {
  if (!user) {
    getAccountDetails(token).then(({ amount, owner: user }) => {
      setUser(user);
      setAmount(amount);
    });
  }
  if (!transactions) {
    getTransactions(token).then(({ result: transactions }) =>
      setTransactions(transactions)
    );
  }
}, [token, user, transactions]);
```

Werden zum Beispiel die `getAccountDetails` geladen und mit `setUser` gespeichert, bevor auch `setTransactions` aufgerufen wird, dann wird der Effekt nochmals ausgeführt.
{% endcapture %}
{% include quiz.html header=q1-header question=q1-question answer=q1-answer %}
