# OntoPortal BioMixer Visualizer

A standalone ontology visualizer for OntoPortal. This project replaces the legacy [BioMixer](https://github.com/thechiselgroup/biomixer) embed while keeping its commonly used query parameters and fullscreen message contract.

The application is plain HTML, CSS, and JavaScript. It can be served directly by a Web server or embedded in OntoPortal Web UI.

## Run locally

```bash
python3 -m http.server 8080
```

Open <http://localhost:8080/>.

A container image can be built and served on port 8000:

```bash
docker build -t biomixer-visualizer .
docker run --rm -p 8000:8000 biomixer-visualizer
```

The container serves both `/` and `/visualizer/`, matching the default OntoPortal deployment ingress path.

## Embed parameters

The visualizer accepts these BioMixer-compatible parameters:

- `mode=embed`
- `embed_mode=paths_to_root|term_neighborhood|mappings_neighborhood|ontology_mapping_overview|uml|diagram|print`
- `ontology_acronym`, `ontology`, or `acronym`
- `full_concept_id`, `conceptid`, or `class_id`
- `userapikey` or `apikey`
- `restURLPrefix`

Optional integrations:

- `sparql_endpoint`, `sparqlEndpoint`, or `sparql`
- `lodview_url`, `lodview`, or `resource_view_url`; use `{iri}` as the encoded resource placeholder

Example:

```text
http://localhost:8080/?mode=embed&embed_mode=paths_to_root&ontology_acronym=STY&full_concept_id=http%3A%2F%2Fpurl.bioontology.org%2Fontology%2FSTY%2FT071&restURLPrefix=https%3A%2F%2Fdata.bioontology.org
```

## OntoPortal integration

OntoPortal Web UI can serve these files itself or point to a separately hosted copy with `ONTOPANEL_VISUALIZER_URL`. The `biomixer_replacement` Flipper feature selects the replacement; the legacy BioMixer embed remains the default until that feature is enabled.

The public widget reads `biomixer_replacement_enabled` and `ontopanel_visualizer_url` from the existing site configuration endpoint.

## Features

- paths-to-root, neighborhood, mappings, ontology atlas, and diagram views
- pan, zoom, node dragging, minimap, search, and keyboard controls
- class details, relations, selection history, and optional SPARQL queries
- SVG, PNG, JSON, diagrams.net, and PlantUML downloads
- print view and light/dark themes
- visible-node limits and paged atlas loading for large ontologies

## Validate

```bash
node --check app.js
```

Open an embed URL and verify that ontology data loads from the configured OntoPortal API.

## License

Apache License 2.0. See [LICENSE](LICENSE).
