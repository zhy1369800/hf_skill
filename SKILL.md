---
author: https://github.com/burugo/one-mcp
description: 'External tools: hf (huggingface mcp)'
mcp_count: 1
name: one-mcp-hf
services:
    - hf
tool_count: 18
version: 1.0.1
---

# hf

## Quick Reference

| Service | Tool | Description |
|---------|------|-------------|
| hf | `hf_whoami` | Hugging Face tools are being used by authenticated user '... |
| hf | `space_search` | Find Hugging Face Spaces using semantic search. IMPORTANT... |
| hf | `hub_repo_search` | Search Hugging Face repositories with a shared query inte... |
| hf | `create_repo` | Create a Hugging Face model, dataset, space, or bucket re... |
| hf | `paper_search` | Find Machine Learning research papers on the Hugging Face... |
| hf | ... | +13 more tools, see [tools/hf.md](tools/hf.md) |

## Available Services

### hf (18 tools)

huggingface mcp

- [View all tools](tools/hf.md)
- Tools: `hf_whoami`, `space_search`, `hub_repo_search`, `create_repo`, `paper_search`, `hub_repo_details`, `hf_doc_search`, `hf_doc_fetch`, `hf_jobs`, `hf_hub_query`, `write_file`, `list_files`, `read_file`, `file_manager`, `0a9f249006af_store_files`, `gr1_z_image_turbo_toggle_seed`, `gr1_z_image_turbo_generate_image`, `gr1_z_image_turbo_generate_image_1`

## How to Use

1. Find the tool you need in the Quick Reference table above
2. Read detailed documentation from `tools/{service-name}.md`
3. Execute using the syntax below

## Execution Syntax

```bash
python executor.py <service-name> <tool-name> '<json-params>'
```

### Example

```bash
python executor.py hf space_search '{"limit":10,"mcp":true,"query":"example search query"}'
```

## Refresh Tool Docs

If the MCP tools change, refresh the docs:

```bash
python refresh_tool_docs.py
```
