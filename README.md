# autodetect_metadata_prototype
my autodetect metadata prototype to showcase on my design portfolio

## Running it

`index.html` is a single self-contained file — no build step, no dependencies.
Open it directly in a browser, or serve the folder:

```
python3 -m http.server
```

then visit http://localhost:8000

## The flow

1. **Uploads tab, empty state** — click **Add** (header or empty-state button)
2. **Upload File** — opens a simulated macOS Finder dialog with a sample set of PDFs
3. **Open** — files upload and the table switches to the populated processing state
4. **Metadata columns** (Description, Type, Revision, Discipline, Originator,
   Classification) show per-cell loading spinners while detection runs. Hovering
   a cell explains what's happening; clicking one takes over manually and stops
   auto-detection for that cell.
5. The **Uploads toast** (bottom right) tracks upload progress and can be
   collapsed or dismissed.
