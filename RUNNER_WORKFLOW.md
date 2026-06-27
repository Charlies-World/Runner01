# Runner01 Image Processing Workflow

Runner01 is the control repo for cross-repo image processing.

## Repos

```text
Charlies-World/Runner01       workflow control
Charlies-World/Software       SoftStrange-ImageEditor code
Charlies-World/PrintImages01  image pipeline folders
```

## Workflow

```text
.github/workflows/process-print-images.yml
```

It is triggered with `workflow_dispatch`, so it can be launched from the GitHub UI, REST API, GitHub CLI, or an MCP server that calls the GitHub API.

## Default test run

Run the workflow with defaults:

```text
source_repo: Charlies-World/PrintImages01
software_repo: Charlies-World/Software
input_folder: image-pipeline/inbox/gizmo-adventure/logos/test-batch
direction_path: direction-white-clean.json
pipeline_root: image-pipeline
generate_test_images: true
```

When the input folder is empty, the workflow creates three synthetic Gizmo test images, runs the image processor, and uploads the whole `image-pipeline` folder as an Actions artifact.

## REST API trigger

```bash
curl -L \
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  https://api.github.com/repos/Charlies-World/Runner01/actions/workflows/process-print-images.yml/dispatches \
  -d '{"ref":"main","inputs":{"generate_test_images":"true"}}'
```

The token needs Actions write permission on Runner01.

## MCP server target tools

A future MCP server should expose these narrow tools:

```text
upload_image_to_print_repo
trigger_runner_workflow
get_runner_workflow_status
get_runner_workflow_logs
list_print_outputs
download_output_artifact
```
