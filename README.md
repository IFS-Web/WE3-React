# Web Engineering 3 – React

Siehe ...

## Development

Um nicht alle Dependencies lokal zu installieren empfiehlt es sich, Jekyll mit Docker zu nutzen:

```bash
docker run --rm  --volume="$PWD:/srv/jekyll:Z" --publish 4000:4000 jekyll/jekyll:4.2.2 jekyll serve -I
```

## Lizenz

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
