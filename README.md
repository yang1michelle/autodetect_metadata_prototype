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
   Classification) show per-cell loading spinners while detection runs. Version
   sits among them but is never detected — it always reads *Pending*. Hovering
   a cell explains what's happening; clicking one takes over manually and stops
   auto-detection for that cell.
5. **Detection lands progressively.** Each field resolves on its own timer, so
   rows fill in unevenly — cells settle while their neighbours are still
   spinning. A detected value drops its input chrome and gains an orange
   sparkle. The **Name** column resolves to an ISO 19650 information container
   ID; where the filename is missing a segment, the ID appears incomplete
   (`PN-__-DR-A-1990`) until the ML pass fills the gap.
6. **Hover a sparkle** to see where the value came from — "extracted from the
   file name" for values parsed out of the container ID, "extracted from the
   file contents" for values read from the drawing's title block.
7. Once every field and the container ID have resolved, **Required Action**
   flips from *Processing* to a **Submit** button.
8. Editing a detected value removes its sparkle (the value is now
   user-corrected); leaving it untouched restores it.
9. Fields that fail take an error state — a red-bordered control with an amber
   warning explaining why detection failed, alongside the data table's own
   required-field error. Required Action becomes **Missing Attributes**, listing
   the missing fields on hover.
10. The **Uploads toast** (bottom right) tracks upload progress and can be
    collapsed or dismissed.

## Scenarios

Append a `scenario` parameter to demo a failure mode:

| URL | Shows |
| --- | --- |
| `index.html` | The normal run — a mix of detected and not-detected fields |
| `index.html?scenario=ml-down` | The ML service unresponsive: rows stay in *Processing*, and after 6s each one shows a **Detection Delayed** warning |
