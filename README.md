# godot-ci


Docker image to export Godot Engine games and deploy to GitLab/GitHub Pages and Itch.io using GitLab CI and GitHub Actions.

Based on [abarichello/godot-ci](https://github.com/abarichello/godot-ci)

## Docker Hub

https://hub.docker.com/r/nicolanore/godot-ci/

## How To Use

You can launch an export with `godot --headless -v --export "HTML5" build/html5/index.html`

Here is an example Github Action to export a project :

```yaml
name: "godot-ci export"
on: push

env:
  GODOT_VERSION: 4.0-beta4
  EXPORT_NAME: restodot

jobs:
  export-web:
    name: Web Export
    runs-on: ubuntu-20.04
    container:
      image: "nicolanore/godot-ci:4.0-beta4"
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          lfs: true
      - name: Setup
        run: |
          mkdir -v -p ~/.local/share/godot/
          ln -s /root/.local/share/godot/export_templates ~/.local/share/godot/export_templates
      - name: Web Build
        run: |
          mkdir -v -p build/html5
          godot --headless -v --export "HTML5" build/html5/index.html
```