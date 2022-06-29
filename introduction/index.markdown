---
title: Einführung
layout: default
nav_order: 2
next: Woche 1
---

# Hello World

<video src="https://tube.switch.ch/external/f20bed87" playsinline controls style="width: 100%"></video>

# Übungen
Um mit React zu starten verwenden wir Create React App. Dazu benötigen Sie nur eine relativ aktuelle NPM-Version, die Sie aus den vorherigen Übungen bereits haben sollten. Erstellen Sie also ein neues Projekt:

```bash
npx create-react-app uebung-1 
```

Und öffnen Sie das erstellte Projekt im Ordner uebung-1 in der IDE oder dem Editor Ihrer Wahl. Auf der Konsole brauchen Sie nur noch npm start auszuführen und Sie sind bereit für die Entwicklung. Lassen Sie die Konsole am besten im Hintergrund geöffnet, so führen Änderungen am Code direkt zu einem Reload im Browser.

Die generierte Projektstruktur ist recht einfach gehalten, umfasst aber schon einen Beispieltest, ein Manifest, etc:

```jsx
function App() {
 return (
   <div className="App">
     <header className="App-header">
       <img src={logo} className="App-logo" alt="logo" />
       <p>
         Edit <code>src/App.js</code> and save to reload.
       </p>
       <a
         className="App-link"
         href="https://reactjs.org"
         target="_blank"
         rel="noopener noreferrer"
       >
         Learn React
       </a>
     </header>
   </div>
 );
}
```

{% assign q1-header = "Quiz" %}
{% assign q1-question = "Inwiefern unterscheidet sich der JSX-Code überhaupt von HTML?" %}
{% capture q1-answer %}
In diesem Beispiel gibt es nur einen Unterschied: anstelle von `class` wird `className` verwendet, da `class` ein **Javascript-Keyword** ist.
{% endcapture %}
{% include quiz.html header=q1-header question=q1-question answer=q1-answer %}



# Komponenten Erstellen

Erstellen Sie als erstes Komponenten (in eigenen Dateien) für die einzelnen Tags, so dass am Ende höchstens noch ein HTML-Tag Pro Komponente vorhanden ist. Die App Komponente könnte dann z.B. noch so aussehen:

```jsx
function App() {
 return (
   <div className="App">
     <Header />
   </div>
 );
}
```

Hier noch ein Beispiel von JSFiddle

<iframe width="100%" height="300" src="//jsfiddle.net/misto/tnmco5fv/embedded/js,result/dark" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

[Link button](http://example.com/){: .btn }
