# hf Tools

## hf_whoami

Hugging Face tools are being used by authenticated user 'zhouyon'

## space_search

Find Hugging Face Spaces using semantic search. IMPORTANT Only MCP Servers can be used with the dynamic_space toolInclude links to the Space when presenting the results.

**Params:**
```yaml
limit:
    default: 10
    desc: Number of results to return
    type: number
mcp:
    default: false
    desc: Only return MCP Server enabled Spaces
    type: boolean
query:
    desc: Semantic Search Query
    required: true
    type: string
```

## hub_repo_search

Search Hugging Face repositories with a shared query interface. You can target models, datasets, spaces, or aggregate across multiple repo types in one call. Use space_search for semantic-first discovery of Spaces. Include links to repositories in your response.

**Params:**
```yaml
author:
    desc: Organization or user namespace to filter by (e.g. 'google', 'meta-llama', 'huggingface').
    type: string
filters:
    desc: Optional hub filter tags. Applied to each selected repo type (e.g. ["text-generation"], ["language:en"], ["mcp-server"]).
    type: array
limit:
    default: 20
    desc: Maximum number of results to return per selected repo type
    type: number
query:
    desc: Search term. Leave blank and specify sort + limit to browse trending or recent repositories.
    type: string
repo_types:
    default:
        - model
        - dataset
    desc: Repository types to search. Defaults to ["model", "dataset"]. space uses keyword search via /api/spaces.
    type: array
sort:
    desc: 'Sort order (descending): trendingScore, downloads, likes, createdAt, lastModified'
    enum:
        - trendingScore
        - downloads
        - likes
        - createdAt
        - lastModified
    type: string
```

## create_repo

Create a Hugging Face model, dataset, space, or bucket repository.

**Params:**
```yaml
name:
    desc: Fully-qualified repository name in 'namespace/repo-name' format.
    required: true
    type: string
private:
    desc: Whether to create the repository as private.
    type: boolean
repo_type:
    default: bucket
    desc: Repository type. Defaults to bucket.
    enum:
        - model
        - dataset
        - space
        - bucket
    type: string
sdk:
    default: static
    desc: SDK type - only required for repo_type='space'.
    enum:
        - streamlit
        - gradio
        - docker
        - static
    type: string
```

## paper_search

Find Machine Learning research papers on the Hugging Face hub. Include 'Link to paper' When presenting the results. Consider whether tabulating results matches user intent.

**Params:**
```yaml
concise_only:
    default: false
    desc: Return a 2 sentence summary of the abstract. Use for broad search terms which may return a lot of results. Check with User if unsure.
    type: boolean
query:
    desc: Semantic Search query
    required: true
    type: string
results_limit:
    default: 12
    desc: Number of results to return
    type: number
```

## hub_repo_details

Get details for one or more Hugging Face repos (model, dataset, or space). Auto-detects type unless specified. For datasets, use operations: overview, dataset_structure, dataset_preview. Use dataset_structure first to discover configs, splits, sizes, and schema. Use dataset_preview only when config and split are known, unless the dataset has a single config/split. README file may be requested from the external repository.

**Params:**
```yaml
config:
    desc: Dataset Viewer config. Required for dataset_preview when the dataset has multiple config/split options. Discover via dataset_structure.
    type: string
include_readme:
    default: false
    desc: Include README from the repo
    type: boolean
limit:
    desc: Row count for dataset_preview. Defaults to 5 and is clamped to 1-100.
    type: integer
offset:
    desc: Row offset for dataset_preview. Defaults to 0.
    type: integer
operations:
    desc: Details to return. Defaults to ["overview"]. For datasets, prefer ["overview", "dataset_structure"] first; then call ["dataset_preview"] with config and split.
    type: array
repo_ids:
    desc: Repo IDs for (models|dataset/space) - usually in author/name format (e.g. openai/gpt-oss-120b)
    required: true
    type: array
repo_type:
    desc: Specify lookup type; otherwise auto-detects
    enum:
        - model
        - dataset
        - space
    type: string
split:
    desc: Dataset Viewer split. Required for dataset_preview when the dataset has multiple config/split options. Discover via dataset_structure.
    type: string
```

## hf_doc_search

Search and Discover Hugging Face Product and Library documentation. Send an empty query to discover structure and navigation instructions. Knowledge up-to-date as at 19 June 2026. Combine with the Product filter to focus results.

**Params:**
```yaml
product:
    desc: Filter by Product. Supply when known for focused results
    type: string
query:
    desc: Start with an empty query for structure, endpoint discovery and navigation tips. Use semantic queries for targetted searches.
    required: true
    type: string
```

## hf_doc_fetch

Fetch a document from the Hugging Face or Gradio documentation library. For large documents, use offset to get subsequent chunks.

**Params:**
```yaml
doc_url:
    desc: Documentation URL (Hugging Face or Gradio)
    required: true
    type: string
offset:
    desc: Token offset for large documents (use the offset from truncation message)
    type: number
```

## hf_jobs

Remote compute for Hugging Face workflows. Run Python/UV or Docker jobs to deeply analyze Hub datasets, repos, traces, models, and large files; compute trends/statistics; run batch inference/evaluation; or perform long-running work with installed libraries. Use for dataset/repo analysis prompts when local chat inspection is insufficient. Includes submit, logs, inspect, cancel, schedule, and volume mounting.

**Params:**
```yaml
args:
    desc: Operation-specific arguments as a JSON object
    type: object
operation:
    desc: 'Operation to execute. Valid values: "run", "uv", "ps", "logs", "inspect", "cancel", "scheduled run", "scheduled uv", "scheduled ps", "scheduled inspect", "scheduled delete", "scheduled suspend", "scheduled resume"'
    enum:
        - run
        - uv
        - ps
        - logs
        - inspect
        - cancel
        - scheduled run
        - scheduled uv
        - scheduled ps
        - scheduled inspect
        - scheduled delete
        - scheduled suspend
        - scheduled resume
    type: string
```

## hf_hub_query

Read-only Hugging Face Hub navigator for discovery, lookup, filtering, ranking, counts, field-constrained extraction, and relationship questions across users, orgs, models, datasets, spaces, collections, discussions, daily papers, recent activity, followers/following, likes, and likers. Good for structured raw outputs and compact results. Generated helper calls can explicitly bound limit, scan_limit, max_pages, and ranking_window for brevity or broader coverage, and the tool can also be asked about its supported helpers, canonical fields, defaults, and coverage behavior.

**Params:**
```yaml
message:
    required: true
    type: string
```

## write_file

Write string content as a file to a Hugging Face bucket, model, dataset, or Space.

**Params:**
```yaml
commit_description:
    default: null
    desc: Optional commit description for repo uploads.
commit_message:
    default: null
    desc: Optional commit message for repo uploads.
content:
    desc: String content to write to the Hub.
    required: true
    type: string
create_if_missing:
    default: true
    desc: |-
        Create the repo or bucket if it does not already exist.
        This matches the default behavior of `hf upload` for repos.
    type: boolean
create_pr:
    default: false
    desc: Open repo uploads as a pull request instead of committing directly.
    type: boolean
encoding:
    default: utf-8
    desc: Text encoding used to convert the string to bytes.
    type: string
path_in_repo:
    desc: File path to create in the repo, or object path in the bucket.
    required: true
    type: string
private:
    default: null
    desc: Optional privacy setting when creating the repo or bucket.
repo_id:
    desc: Hub repo id, or bucket id when repo_type is bucket.
    required: true
    type: string
repo_type:
    default: model
    desc: 'Repository type: model, dataset, space, or bucket.'
    enum:
        - model
        - dataset
        - space
        - bucket
    type: string
revision:
    default: null
    desc: Branch or revision for repo uploads.
space_sdk:
    default: static
    desc: Space SDK to use when creating a Space.
    enum:
        - static
        - gradio
        - streamlit
        - docker
    type: string
```

## list_files

List uploaded Hugging Face Bucket files with metadata and HTTPS URLs usable as Gradio File Inputs.

## read_file

Read an uploaded Hugging Face Bucket file by name and return its contents plus an HTTPS URL usable as a Gradio File Input.

**Params:**
```yaml
name:
    required: true
    type: string
```

## file_manager

Upload and manage files. Drop files here to send them to the server.

## 0a9f249006af_store_files

FastMCP app backend action discovered from file_manager.

**Params:**
```yaml
files: {}
```

## gr1_z_image_turbo_toggle_seed

Z_Image_Turbo_toggle_seed tool (from mrfakename/Z-Image-Turbo)

**Params:**
```yaml
randomize:
    default: true
    type: boolean
```

## gr1_z_image_turbo_generate_image

Generate an image from the given prompt. (from mrfakename/Z-Image-Turbo)

**Params:**
```yaml
height:
    default: 1024
    type: number
num_inference_steps:
    default: 9
    type: number
prompt:
    type: string
randomize_seed:
    default: true
    type: boolean
seed:
    default: 42
    type: integer
width:
    default: 1024
    type: number
```

## gr1_z_image_turbo_generate_image_1

Generate an image from the given prompt. (from mrfakename/Z-Image-Turbo)

**Params:**
```yaml
height:
    default: 1024
    type: number
num_inference_steps:
    default: 9
    type: number
prompt:
    type: string
randomize_seed:
    default: true
    type: boolean
seed:
    default: 42
    type: integer
width:
    default: 1024
    type: number
```

