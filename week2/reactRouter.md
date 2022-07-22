---
title: React Router
parent: Woche 2
nav_order: 5
previous: Data Loading
---

# React Router

Als Abschluss dieser Übung und als Vorbereitung auf die Übungen und die Bearbeitung des Testats nächste Woche schauen wir uns den Aufbau des React-Routers genauer an.

## Routing in React

React-Router ist bereits seit einigen Jahren ein weit verbreitetes und benutztes Tool, um effizientes Routing in Web Applikation zu ermöglichen.

React Router hat drei grundlegende Komponenten:

- Routers
- Route Matchers
- Navigation Elements

### Routers

Für Webapplikationen stehen zwei Router zur Verfügung. `<BrowserRouter>` und `<HashRouter>`.

{% assign q1-header = "Quiz" %}
{% assign q1-question = "Welcher Router wird in der BOR Applikation benutzt und wo ist diese zu finden? Wieso wird diese Stelle für den Router gewählt?" %}
{% capture q1-answer %}
Die BOR Applikation verwendet den `<BrowserRouter>`.
Angewendet wird der Router im `index.js`.
Die Router Komponente managed die Handhabung und das Rendering der verschiednen Komponenten einer Applikation und befindet sich deshalb am Einstiegspunkt aller Komponenten. Der Router umschliesst die top-Level `<App>` Komponente und kann somit die gesamte Applikation "steuern".

```jsx
import { BrowserRouter } from 'react-router-dom';
...

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <BrowserRouter >
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

{% endcapture %}
{% include quiz.html header=q1-header question=q1-question answer=q1-answer %}

{% assign q2-header = "Quiz" %}
{% assign q2-question = "Was ist der Unterschied zwischen `<BrowserRouter>` und `<HashRouter>`? Entscheid anhand deiner Recherche, ob der momentan benutze Router für die BOR Applikation geignet ist." %}
{% capture q2-answer %}
`<BrowserRouter>`: Benutzt reguläre URL Pfade. Kann für server- und clientseitiges Rendering benutzt werden. Serverseitiges Rendering setzt die korrekte Konfiguration der Routen auf Client und Server voraus.

`<HashRouter>`: Benutzt URL Pfade mit Hashtag, zum Beispiel: http://example.com/#/page. Das '#' wird nicht an den Server geschickt und es braucht daher auch keine spezielle serverseitige Konfiguration.

Für die BOR Applikation können beide Router benutzt werden. Da jedoch keine Pages serverseitig generiert und die Daten durch gezielte Request abgefragt werden, kann durchaus ein `<HashRouter>` benutzt werden.

```jsx
import { HashRouter } from 'react-router-dom';
...

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <HashRouter >
      <App />
    </HashRouter>
  </React.StrictMode>
);
```

{% endcapture %}
{% include quiz.html header=q2-header question=q2-question answer=q2-answer %}

### Route Matchers

Es gibt zwei Komponenten, die sich um das Matching der URL kümmert, `<Switch>` und `<Route>`.

`<Switch>` durchsucht seine untergeordneten `<Route>` Komponenten und wählt diejenige, welche auf die momentane URL passt. Falls es eine findet, wird diese `<Route>` Komponente gerendert und die restlichen Routen werden ignoriert.

Wichtig zu beachten ist, dass längere bzw. spezifischere Routen **vor** weniger spezifischeren Routen gesetzt werden müssen. Das einfachste Beispiel dafür ist `<Route path='/'>`. DIese Route matchet der URL **immer**! Daher wird diese Route innerhalb einer `<Switch>`Komponente als letztes definiert.

Die einfachste Art und weise diese Routen Ordnung zu Umgehen, ist das setzt des props `exact`. Eine `<Route exact path='/path/blabla/>` Komponente wird gerendert, sobald die URL genau mit dem Pfad übereinstimmt, egal wo diese im `<Switch>` platziert ist.

Hier ist ein Beispiel der Entwickler des React Routers:

```jsx
function App() {
  return (
    <div>
      <Switch>
        {/* If the current URL is /about, this route is rendered
            while the rest are ignored */}
        <Route path="/about">
          <About />
        </Route>

        {/* Note how these two routes are ordered. The more specific
            path="/contact/:id" comes before path="/contact" so that
            route will render when viewing an individual contact */}
        <Route path="/contact/:id">
          <Contact />
        </Route>
        <Route path="/contact">
          <AllContacts />
        </Route>

        {/* If none of the previous routes render anything,
            this route acts as a fallback.

            Important: A route with path="/" will *always* match
            the URL because all URLs begin with a /. So that's
            why we put this one last of all */}
        <Route path="/">
          <Home />
        </Route>
      </Switch>
    </div>
  );
}
```

**WICHTIG**: Die BOR Applikation verwendet `react-router-dom` Version 6.3.0. Darin wurde `<Switch>` durch `<Routes>` ersetzt. Ausserdem werden die zu rendernden Komponenten in `<Route>` nicht als Kinder, sonder als Props übergeben.

### Navigation

Die Navigation wird durch die `<Link>` oder `<NavLink>` Komponente zur Verfügung gestellt. Dabei ist `<NavLink>` die spezielle Variante von `<Link>` die sich je nach aktiver URL stylen lässt.

Die BOR Applikation ermöglicht die Navigation in der Menu Leiste.

```jsx
const MenuBar = () => {
  return (
    <Container>
      <Card style={{ marginTop: "1rem" }}>
        <Navbar color="light" expand="md" light>
          <NavbarBrand href="/">
            {user.firstname} {user.lastname} - {user.accountNr}
          </NavbarBrand>
          <Nav className="mr-auto" pills>
            <NavItem>
              <NavLink
                tag={Link}
                active={pathName === "/dashboard"}
                to={"/dashboard"}
              >
                Dashboard
              </NavLink>
            </NavItem>
          </Nav>
          <Nav className="mr-auto" style={{ marginLeft: "auto" }} pills>
            <NavItem>
              <NavLink href="/" onClick={signout}>
                Logout {user.firstname} {user.lastname}{" "}
              </NavLink>
            </NavItem>
          </Nav>
        </Navbar>
      </Card>
    </Container>
  );
};
```

## Testat Vorbereitung

{% assign t1-header = "Task" %}
{% assign t1-question = "Die BOR Applikation braucht eine weitere Route.
 Erstelle eine neue Komponente `transactions`, eine Route auf für diese Komponente und füge einene neuen Link in der Menuleiste hinzu." %}
{% assign t1-hint = "Die Transaktions Komponente kann leer sein. Aber achte darauf, dass die Funktionalität beim Wechsel zwischen Dashboard und Transaktion sichergestellt ist.  " %}
{% include task.html header=t1-header task=t1-question  hint=t1-hint %}


{% assign s-header = "Solution" %}
{% assign s-solution = "https://gitlab.ost.ch/etienne.baumgartner/bor_final/-/compare/data_loading_solution...react_router_solution?from_project_id=4572" %}
{% include solution.html solution=s-solution %}