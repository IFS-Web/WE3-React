---
title: Testat
nav_order: 6
has_children: true
previous: Woche 3
---

# Testat

Für das Testat steht ein Assignment auf GitHub Classroom bereit. Die Ausgangslage ist dabei die Solution des vorhergehenden Schritts.

Für das Testat sollen Sie folgende zwei Aufgaben lösen:

## Gebrauch vom Redux Store

Im Moment werden verschiedne Objekte und Werte als Props in `App.js` an die Unterkomponenten mitgegeben. Schreibe für diese Props passende **_Reducers, Actions und Slices_**. Entferne die Props und verbinde die Komponenten (Home, Dashboard, etc.) direkt mit dem Redux-Store.

{% assign t2-header = "Task" %}
{% assign t2-question = "Integriere die React States in den Redux Store.  
Anbei eine Liste der Props, welche mindestens in den Redux State verlegt werden müssen:

- User
- Token
- isAuthenticated
- Transactions" %}
  {% assign t2-hint = "
  Achte auf folgende Dinge:
- Erstelle einen `transactionSlice`. Orientiere dich dabei am `loginSlice.js
- `isAuthenticated` kann dem bestehenden `loginSlice` hinzugefügt werden und braucht keinen eigenen Slice.
- User, Token und isAuthenticated States sollen bei Page Reload wieder gesetzt werden. Überlege dir, wie dies mit dem `useEffect`-Hook und dem `sessionStorage` verbunden werden kann.

  " %}
  {% include task.html header=t2-header task=t2-question  hint=t2-hint %}

## Transaktions Komponente

Erweitere die `Transactions`-Komponente anhand untenstehendem Abbild.

<p align='center'>
<img src='img/transactions.png' alt='action_dispatch_store'/>
</p>

{% assign t2-header = "Task" %}
{% assign t2-question = "
Erweitere die Transaction Komponente.

Um die Implementierung zu vereinfachen, werden drei Files zur Verfügung gestellt.

- MonthDropdown
- YearDropDown
- PaginatedTransactionTable

Füge diese Files dem `./src/components` Ordner der BOR Applikation hinzu und benutze diese Templates zur Erstellung der `Transactions`-Komponente.

<a href='./files/TestatFiles.zip' download='TestatFiles.zip'>Files Herunterladen</a>

" %}
{% assign t2-hint = "
Da es sich bei diesem Task um eine grössere Übung handelt, geben wir anbei eine Anleitung für die vorzunehmenden Schritte:

**1. Fetching der Transaktionen**

- Nutze `api.js`, um die Transaktionen abzufragen und speichere die Response in den Redux Store mit Hilfe der Aktionen, welche Du im vorherigen Schritt erstellt hast.

  **Beachte:** Die `getTransactions(...)` Funktion enthält Argumente, mit welchen Du beinflussen kannst, welche Transaktionen abgefragt werden. Dies wird später nochmals wichtig für die Filterung der Transaktionen.

- Implementiere die Abfrage in einer eigenen Funktion, um diese später wiederverwenden zu können.

**2. Einbinden der `PaginatedTransactionsTable`-Komponente mit Props:**

- `total` soll zusammen mit den Transaktionen im Redux Store abgelegt werden. Die untenstehende Abfrage zeigt auf, wie Du an den Wert kommst:

```jsx
getTransactions(token, fromDate, toDate, itemsPerPage, skip).then(
  ({ result: transactions, query: { resultcount } }) => {
    // add transactions to redux store
    // add resultcount to redux store

    // resultcount is the total of all transactions in database
  }
```

- `skip` beschreibt wieviele Transaktionen bei einer Abfrage übergangen wurden. Kann im React State gehalten werden. Das Intervall soll auf 10 Transaktionen beschränkt werden.
- `onForward` / `onBack` beschreiben die angewendeten Funktionen beim Betätgen der Navigation in der Tabelle. Diese Funktionen verändern den `skip` Wert.  
  **Beachte**: Falls die Tabelle vorwärts/rückwärts navigiert wird, müssen ebenfalls die neuen Transaktionen abgefragt werden.

**3. Filter**

- Integriere `MonthDropdown` und `YearDropdown`
- `fromDate` und `toDate` sollen als `ISOString` der `getTransaction(...)`-Funktion übergeben werden.  
  Benutze das folgende Template:

```jsx
fromDate = Moment(`01-01-2000`, 'D-M-YYYY').toISOString();
```

Ersetzte die passenden Stellen im Datums String mit dem Filter (Monat bzw. Jahr).

- Die Filter sollen beim Fetch der Transaktionen neu berechnet und anschliessend der Anfrage mitgegeben werden. `skip` zurücksetzen nicht vergessen!
- Jedes Mal wenn ein Filter gesetzt oder eine 'Seite umgeblättert' wird, muss eine neue Abfrage gestartet werden.
- Stell sicher, dass dem Benutzer angezeigt wird, falls keine Transaktionen für ein Filterkombination gefunden wurde (siehe _Conditional Rendering_)
- **Beachte:** Monate haben unterschiedliche Anzahl Tage.

**4. Styling**

- Nutze `reactstrap` Komponenten wie `Card`, `Row`, `Col`, etc.

" %}
{% include task.html header=t2-header task=t2-question  hint=t2-hint %}

## Refactoring und Cleanup

Vereinfache wo möglich Komponenten und entferne nicht mehr verwendeten Code.

## Abgabe

**Die Abgabe muss bis am 19.10.2022 um Mitternacht committed und auf GitHub gepusht werden.**
