---
title: React Redux
parent: Woche 3
nav_order: 3
previous: Redux
next: Testat
---

# React Redux

Nun kennst du die Grundlagen von Redux und es ist an der Zeit diese in unsere BOR Applikation zu integrieren.

React stellt spezifische Packages zur Entwicklung mit Redux zur Verfügung.

## Installation

`npm install react-redux`

Dieses Package enthält die offiziellen React Binidngs für Redux.

`npm install @reduxjs/toolkit`

Das Redux Tool Kit haben wir im vorherigen Abschnitt bereits vorgestellt. Es vereinfacht die Entwicklung mit Redux.

## Redux Store Setup

{% assign t1-header = "Task" %}
{% assign t1-question = "Erstelle ein neues File `store.js` mit einem vorerst leeren **_Reducer_**." %}
{% assign t1-hint = "Benutze die `configureStore` API des Redux Toolkits. (Siehe vorheriger Abschnitt)" %}
{% include task.html header=t1-header task=t1-question  hint=t1-hint %}

Dieses Objekt beinhaltet den **Store** der BOR Applikation. Ein weiterer Vorteil des Redux Toolkits ist, dass durch diese Konfiguration die DevTools Extensions automatisch miteinbezogen werden und die Webentwicklung dadurch trivialer wird. Stelle sicher, dass du die Redux Devtool Browser Extension in deinem Browser installiert hast.

Als zweiter Schritt soll der **Store** in der React Applikation als Provider eigebunden werden:

{% assign q1-header = "Quiz" %}
{% assign q1-question = "Wie und an welcher Stelle in der BOR Applikation, bzw. in einer React Applikation, soll der Store am Besten eingebunden werden? " %}
{% capture q1-answer %}
Der Redux Store enthält State einer Applikation.
Dieser State wird global gehalten und sollte daher im `index.js` eigebunden werden.

Die Einbindung wird durch die `Provider` Schnittstelle des `react-redux` Packages ermöglicht und umschliesst die `<App>` Komponente.
{% endcapture %}
{% include quiz.html header=q1-header question=q1-question answer=q1-answer %}

{% assign t2-header = "Task" %}
{% assign t2-question = "Binde den **Store** in die BOR Applikation ein." %}
{% assign t2-hint = "Benutze die `Provider` API von `react-redux`." %}
{% include task.html header=t2-header task=t2-question  hint=t2-hint %}

{% assign s-header = "Lösung" %}
{% assign s-solution = "
`store.js`

```jsx
import { configureStore } from '@reduxjs/toolkit';

const store = configureStore({
  reducer: {},
});

export default store;
```

`index.js`

```jsx
...
import { Provider } from 'react-redux';
import store from './store';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </Provider>
  </React.StrictMode>
);
```

Öffne die Applikation im Browser. Der Store sollte nun in den Redux Dev Tools initialisiert sein.  
Unter Firefox sieht das so aus:

 <p align='center'>
<img src='img/store_init.png' alt='action_dispatch_store'   />
</p>

Achte darauf, dass noch keine Reducer definiert sind und es deshalb zu Fehlermeldungen in der Konsole kommt.

" %}
{% include solution.html solution=s-solution header=s-header %}

## Redux State Slice

Der **Store** ist nun erfolgreich initialisiert. Der nächste Schritt ist das Erstellen eines **States** und die dazugehörigen _puren_ **_Reducer_**-Funktionen, um den State zu verändern.

Um diese Funktionalität aufzuzeigen, wird ein State Slice für den angemeldeten Benutzer erstellt.

{% assign t3-header = "Erstellen eines Slices mit **_Aktionen_** und **_Reducer_**-Funktionen." %}
{% assign t3-question = "
`./redux/loginSlice.js`

```jsx
import { createSlice } from '@reduxjs/toolkit';

export const loginSlice = createSlice({
  name: 'login',
  initialState: {
    user: {},
    token: '',
  },
  reducers: {
    addUserToState: (state, action) => {
      state.user = action.payload.user;
      state.token = action.payload.token;
    },
    removeUserFromState: (state) => {
      state = { user: {}, token: '' };
    },
  },
});

export const { addUserToState, removeUserFromState } = loginSlice.actions;
export const loginReducer = loginSlice.reducer;
```

Der `loginReducer` muss nun der **Store** Konfiguration hinzugefügt werden:

`store.js`

```jsx
import { configureStore } from '@reduxjs/toolkit';
import { loginReducer } from './redux/loginSlice';

const store = configureStore({
  reducer: { login: loginReducer },
});

export default store;
```

Diese Änderungen haben nun den **Store** mit einem _LoginSlice_ erweitert. Überprüfe in deinem Redux Browser Dev Tool, dass ein initiales `login`-Objekt vorhanden ist.

" %}
{% assign t3-hint = "
Ist dir bei den beiden Funktionen im Reducer etwas aufgefallen?  
Die `addUserToState`-Funktion ist nicht **pure**! In _plain Redux_ sollte dies nicht so gelöst werden, aber mit dem _Redux Toolkit_ geht das in Ordnung, da durch eine integrierte Library die mutierten States in einen vollkommen neuen State umgewandelt werden und somit die Funktion durchaus pure ist!  
Ein weitere Vereinfachung für den Anwendeung des Redux Toolkits.

" %}
{% include task.html header=t3-header task=t3-question  hint=t3-hint %}

Der **Store** wurde erfolgreich mit einem initialen `login` Objekt erweitert. Der nächste Schritt ist das Einbinden der `react-redux`-Hooks `useSelector` und `useDispatch`, woauch immer diese Values gebraucht werden.

{% assign t2-header = "Task" %}
{% assign t2-question = "Ersetze den *React State* für `user` und `token` in `App.js` mit den Values aus dem Redux Store." %}
{% assign t2-hint = "Benutze die `useSelector` und `useDispatch` API von `react-redux`.

Beispiel für **_Selektieren_** (Lesen) des Users aus dem Store:

```jsx
const user = useSelector((state) => {
  state.login.user;
});
```

Ein **_Dispatch_** wird folgendermassen initiiert:

```jsx
  const dispatch = useDispatch();
  ...

  // woauch immer eine Änderung auf dem Store durchgeführt werden muss:
  dispatch(<reducerFunction>({<actionPayload>}))
```

" %}
{% include task.html header=t2-header task=t2-question  hint=t2-hint %}

{% assign s-header = "Lösung" %}
{% assign s-solution = "

```jsx
const App = () => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  //const [user, setUser] = useState(JSON.parse(sessionStorage.getItem('user')));
  //const [token, setToken] = useState(sessionStorage.getItem('token'));
  const [pathName, setPathName] = useState(null);
  let location = useLocation();

  const dispatch = useDispatch();

  const user = useSelector((state) => state.login.user);
  const token = useSelector((state) => state.login.token);

  const authenticate = (login, password, callback) => {
    api
      .login(login, password)
      .then(({ token, owner }) => {
        setIsAuthenticated(true);
        //setToken(token);
        //setUser(owner);

        dispatch(addUserToState({ user: owner, token }));

        sessionStorage.setItem('token', token);
        sessionStorage.setItem('user', JSON.stringify(owner));
      })
      .catch((error) => callback(error));
  };

  const signout = () => {
    setIsAuthenticated(false);
    //setToken(undefined);
    //setUser(undefined);

    dispatch(removeUserFromState());

    sessionStorage.removeItem('token');
    sessionStorage.removeItem('user');
  };
  ...
}
```

" %}
{% include solution.html solution=s-solution header=s-header %}

Nun bist Du besetens gerüstet, um dich ans Testat zu machen;)
