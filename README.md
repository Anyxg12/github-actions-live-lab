# GitHub Actions · EXPOGIT

Presentación didáctica en Slidev sobre CI, fallo controlado, corrección y publicación en GitHub Pages.

## Trabajar localmente

```bash
npm ci
npm run dev
```

Edita `slides.md` para cambiar el contenido y `style.css` para ajustar el diseño. Las notas de exposición están en los comentarios al final de cada diapositiva. En Slidev usa el modo presentador para leerlas.

## Comprobar y publicar

```bash
npm run build -- --base /github-actions-live-lab/
git add slides.md style.css
git commit -m "docs: actualizar presentación"
git push origin main
```

`ci.yml` comprueba cada push a main y cada pull request hacia main. `deploy.yml` espera a que CI termine y publica solo si pasó y proviene de un push del propio repositorio. Descarga el mismo commit que comprobó CI. Dentro de Pages, `needs: build` hace esperar al job de publicación. La ejecución manual compila y publica el commit seleccionado.

Sitio: https://anyxg12.github.io/github-actions-live-lab/

## Ensayo recomendado

1. Cambia un título de `slides.md`, guarda, crea un commit y haz push. Muestra CI, Pages y el título publicado.
2. En `package.json`, cambia solo el script build a `slidev build diapositiva-inexistente.md`. Haz commit y push. Muestra el fallo en Compilar presentación y el despliegue omitido. El sitio anterior sigue disponible.
3. Restaura `slidev build`, guarda, crea otro commit y haz push. Muestra CI en verde y la publicación.

Los cambios a package.json se preparan con `git add package.json`. No modifiques el lockfile para este ensayo. Antes y después revisa `git status`. Un re-run ejecuta el mismo commit y no sustituye la corrección.
