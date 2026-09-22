# Findings

No final security verdict has been established.

## F-000 — Research framework

**Date:** 21 September 2026  
**Status:** Established

**Fact:** A controlled security research workflow was defined.

**Observation:** The project can be investigated by comparing baseline and post-operation state.

**Hypothesis:** Differential observation will make it easier to distinguish expected runtime behavior from unexpected behavior.

**Finding:** The methodology is suitable for continuing controlled testing.

**Next Action:** Continue with controlled operations and source correlation.

## F-001 — Hydra runtime HTTPS

**Date:** 21 September 2026  
**Status:** Observed; requires continued correlation

**Fact:** Hydra/Electron processes had established HTTPS connections during normal runtime.

**Observation:** The connections were associated with Hydra Electron processes.

**Hypothesis:** These connections support normal application/backend functionality.

**Finding:** Not yet a security finding; endpoint purpose should be correlated with application behavior and source code.

**Next Action:** Map endpoints to documented application functions and source code.

## F-002 — Third-party source separation

**Date:** 21 September 2026  
**Status:** Methodological finding

**Fact:** A community download source was configured in Hydra.

**Observation:** The source is outside the Hydra codebase.

**Finding:** Source configuration, download infrastructure, and downloaded software must be analyzed as separate trust boundaries.

**Next Action:** Perform controlled tests without conflating third-party file behavior with Hydra behavior.
