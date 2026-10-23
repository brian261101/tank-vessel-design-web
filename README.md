# Tank / vessel design calculator (web)

Static page that runs steps 1-8 of the `tank-vessel-design` Claude Code skill in the browser:
design request form → input validation → design basis → ASME VIII-1 / API 650 calculation →
verification → release gate → calculation PDF, plus a handoff zip.

The calculation is the skill's own Python engine (`pv_design`, version 0.1.0, fingerprint
`40f304ac5576f48f`), run by Pyodide; nothing is reimplemented in JavaScript and no data leaves the browser.

Give the handoff zip to Claude Code with the skill installed and say "use /tank_design to continue
from this handoff". It runs `python pv_design/pv.py resume <zip> --out pv_design/output/<ID>`, recomputes
locally, checks every hash and only then continues with step 9 (FreeCAD model through the MCP),
10 (2D drawings and BOM), 11 (consistency) and 12 (package).

Results are preliminary engineering calculations, never fabrication-ready: the highest stage the
software can reach is CALCULATION_VERIFIED, and release needs review and signature by a qualified engineer.

Built by `pv_design/web/build.py`; do not edit the files here by hand.
