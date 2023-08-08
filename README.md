# holi Development Documentation Entrypoint

This is our website/documentation for people interested in co-creating holi in the area of software development. It's a Jekyll website. View it live at https://app.gitlab-pages.holi.team

---

## Using Jekyll locally

To work locally with this project, you'll have to follow the steps below:

1. Fork, clone or download this project
1. Run `docker run --rm --volume="$PWD:/srv/jekyll:Z" --publish 4000:4000 jekyll/jekyll:3.8 jekyll serve -l`
1. Add content
1. Check your changes in the browser at https://localhost:4000/