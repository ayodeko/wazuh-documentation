# CAT API Documentation Discrepancies Report

## Overview
This report documents critical discrepancies between the source documentation (white theme) and the rendered documentation (dark theme) for Wazuh CAT API operations. The source document should be considered the **source of truth**.

## Critical Issues Summary

### Pattern of Systemic Issues
1. **Missing default values** across all operations
2. **Data type inconsistencies** for array/string parameters
3. **Missing parameters** entirely (especially in Indices operation)
4. **Description truncation/modification** losing important details
5. **Missing Wazuh-specific context** in descriptions

---

## 1. Indices Operation (`/_cat/indices`)

### Missing Parameters (CRITICAL)
The rendered version is **missing the following parameters entirely**:
- `expand_wildcards` - Critical parameter for wildcard matching
- `help` - Help information parameter  
- `include_unloaded_segments` - Memory segment parameter
- `local` - Local node information parameter
- `pretty` - Human-readable format parameter

### Data Type Discrepancies
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `h` | `string or Array of strings` | `Array of strings` | **HIGH** - Breaks API compatibility |

### Missing Default Values
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `help` | `Default: false` | Missing | Medium |
| `include_unloaded_segments` | `Default: false` | Shows default | ✓ Correct |
| `local` | `Default: false` | Missing | Medium |
| `pri` | `Default: false` | Shows default | ✓ Correct |
| `v` | `Default: false` | Missing | Medium |
| `pretty` | `Default: false` | Shows default | ✓ Correct |

### Description Issues
| Parameter | Issue | Impact |
|-----------|-------|---------|
| `bytes` | Source shows concise valid values list, rendered has examples but loses format | Medium |
| `expand_wildcards` | **MISSING ENTIRELY** - Complex parameter with detailed wildcard options | **CRITICAL** |

---

## 2. Cluster Manager Operation (`/_cat/cluster_manager`)

### Data Type Discrepancies
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `h` | `string or Array of strings` | `Array of strings` | **HIGH** |
| `s` | `string or Array of strings` | `string` | **HIGH** |

### Missing Default Values
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `help` | `Default: false` | Missing | Medium |
| `local` | `Default: false` | Missing | Medium |
| `v` | `Default: false` | Missing | Medium |

### Description Changes
| Parameter | Source | Rendered | Impact |
|-----------|---------|----------|---------|
| `local` | "Returns local information but does not retrieve the state from the cluster manager node" | "Whether to return information from the local node only instead of from the cluster manager node" | Medium - Meaning slightly altered |

---

## 3. Nodeattrs Operation (`/_cat/nodeattrs`)

### Data Type Discrepancies
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `h` | `string or Array of strings` | `Array of strings` | **HIGH** |
| `s` | `string or Array of strings` | `string` | **HIGH** |

### Missing Default Values
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `help` | `Default: false` | Missing | Medium |
| `local` | `Default: false` | Missing | Medium |
| `v` | `Default: false` | Missing | Medium |

### Description Issues
| Parameter | Source | Rendered | Impact |
|-----------|---------|----------|---------|
| `cluster_manager_timeout` | "The amount of time allowed to establish a connection to the **Wazuh indexer** cluster manager node" | "A timeout for connection to the cluster manager node" | Medium - Missing Wazuh context |
| `local` | "Returns local information but does not retrieve the state from the **Wazuh indexer** cluster manager node" | "Whether to return information from the local node only instead of from the cluster manager node" | Medium - Missing Wazuh context |

---

## 4. Nodes Operation (`/_cat/nodes`)

### Data Type Discrepancies
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `h` | `string or Array of strings` | `Array of strings` | **HIGH** |
| `s` | `string or Array of strings` | `string` | **HIGH** |

### Missing Default Values
| Parameter | Source Document | Rendered Document | Impact |
|-----------|----------------|-------------------|---------|
| `help` | `Default: false` | Missing | Medium |
| `v` | `Default: false` | Missing | Medium |

### Description Changes
| Parameter | Source | Rendered | Impact |
|-----------|---------|----------|---------|
| `bytes` | "Valid values are: b, kb, k, mb, m, gb, g, tb, t, pb, p" | Extended description with full names but different format | Medium |
| `time` | "Valid values are: nanos, micros, ms, s, m, h, d" | Extended description with full names | Medium |

---

## Impact Assessment

### CRITICAL Issues (Potential Loss of Life/Property)
1. **Missing `expand_wildcards` parameter** in Indices operation - This parameter is essential for index pattern matching and could lead to:
   - Incorrect index queries
   - Missing critical security alerts
   - System monitoring failures

### HIGH Impact Issues
1. **Data type inconsistencies** for `h` and `s` parameters across all operations
   - Breaks API compatibility
   - Could cause integration failures
   - May result in incorrect parameter parsing

### Medium Impact Issues
1. Missing default values
2. Description changes losing context
3. Missing Wazuh-specific terminology

---

## Recommendations

### Immediate Actions Required
1. **Restore missing parameters** in Indices operation (especially `expand_wildcards`)
2. **Fix data type definitions** for `h` and `s` parameters across all operations
3. **Add missing default values** for boolean parameters
4. **Restore complete descriptions** with proper Wazuh context

### Source Location
The API specification appears to be sourced from:
`https://raw.githubusercontent.com/wazuh/wazuh/master/api/api/spec/spec.yaml`

### Next Steps
The CAT API documentation discrepancies need to be fixed in the main Wazuh repository's API specification file, not in this documentation repository.

---

## File Impact
This documentation repository pulls API specs from the main Wazuh repository via:
- `/workspace/source/_variables/settings.py` (line 27)
- API specification URL: `https://raw.githubusercontent.com/wazuh/wazuh/master/api/api/spec/spec.yaml`

**The fixes must be made in the main Wazuh repository's API specification file.**