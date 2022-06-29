---
title: Conditional Rendering
parent: Woche 2
nav_order: 2
previous: Einführung
next: Session Storage
---

# Conditional Rendering

Conditional Rendering erlaubt das Rendering von Teilen einer Komponente, abhängig vom Komponenten State.

React reference: https://reactjs.org/docs/conditional-rendering.html

Beispiel:

```jsx
const Example = () => {
  const [show, setShow] = useState(false);

  return (
    <div>
      {show && <div> Content to show. </div>}
      <button onClick={() => setShow(!show)}>Show Content </button>
    </div>
  );
};
```

Zum Einstieg und um uns ein wenig mit der Applikation vertraut zu machen wollen wir die Applikation ein wenig aufpeppen. Vielleicht ist es Ihnen auch schon aufgefallen: Beim Login gibt es keine Indikation, ob nach dem Klick überhaupt was passiert.

{% assign t1-header = "Task" %}
{% assign t1-question = "Fügen Sie einen Loading Indikator als Button Content hinzu. Benutzen Sie Conditional Rendering." %}
{% assign t1-hint = "Überlegen Sie sich, bei welchem Ereignis die der Loading State geändert werden sollte und setzen Sie diesen mit Hilfe der setState Methode" %}
{% include task.html header=t1-header task=t1-question  hint=t1-hint %}

Ausserdem wäre es wünschenswert, dass falsch eingegebene Anmeldedaten eine visuelles Feedback hinterlassen.  
Dies soll in einer eigenständigen *Card* dargestellt werden. 

{% assign t2-header = "Task" %}
{% assign t2-question = "Fügen Sie eine weitere Card hinzu, welche den User im Falle eines Fehlers im Loginprozess informiert. Benutzen Sie Conditional Rendering." %}
{% assign t2-hint = "Betrachten Sie die authenticate Funktion, welche der Komponente als Prop mitgegeben wurde. Setzt Sie dort an der richtigen Stelle den Error Zustand." %}
{% include task.html header=t2-header task=t2-question  hint=t2-hint %}

{% assign s-header = "Solution" %}
{% assign s-solution = "https://gitlab.ost.ch/etienne.baumgartner/bor_final/-/compare/initial...conditional_rendering_solution?from_project_id=4572" %}
{% include solution.html solution=s-solution %}

