# Claude Command: Commit

Automated commit creation with conventional commit messages.

## Usage

```bash
/commit         # Run without linting (default)
/commit --lint  # Run with linting
```

## Workflow

1. **Linting** (only with `--lint`):
   ```bash
   source .venv/bin/activate && ruff check && ruff format
   ```

2. **Staging Check**:
   - Runs `git status` to check staged files
   - **Stops if 0 files staged** - stage files first with `git add`

3. **Diff Analysis**:
   - Performs `git diff --cached` on staged changes
   - Analyzes for logical separation opportunities
   - Suggests commit splits if multiple concerns detected

4. **Commit Creation**:
   - Generates conventional commit message(s)
   - Executes commit(s) based on analysis

## Conventional Commit Types

- `feat`: New feature (api endpoints, gradio demos, integrations)
- `fix`: Bug fix (concurrency, memory leaks, edge cases)
- `docs`: Documentation only (api docs, deployment guides, readme)
- `style`: Formatting, no code change
- `refactor`: Code restructuring, no behavior change
- `perf`: Performance improvement (speed, memory, concurrency)
- `test`: Test additions/corrections (pytest, integration, load tests)
- `mlops`: Build/tooling/CI changes (github actions, docker, pypi)

## Commit Message Rules

- Format: `<type>: <description>`
- Present tense, imperative mood
- First line ≤ 72 characters
- No emojis

## Split Criteria

Commits are split when detecting:
- Unrelated API/service changes
- Mixed change types (feature + performance optimization)
- Different file categories (src vs tests vs docs vs configs)
- Large changes (>100 lines per file or new service implementation)
- Independent components (api vs ui vs deployment vs ci)

## Examples

### Single Commits
```
feat: add concurrent model inference with asyncio pool
fix: resolve race condition in fastapi endpoint handlers
docs: update gradio demo deployment instructions
refactor: remove duplicate preprocessing logic from pipeline
perf: optimize batch processing with numpy vectorization
test: add pytest fixtures for api endpoint testing
mlops: configure github actions for package publishing
style: apply ruff formatting to inference modules
feat: implement redis caching for model predictions
fix: handle multiprocessing deadlock in worker pool
perf: reduce docker image size from 2gb to 800mb
docs: add openapi schema for all endpoints
test: add benchmarks for concurrent request handling
refactor: extract common validation logic to utils
mlops: add pre-commit hooks for code quality
fix: prevent memory leak in gradio interface callbacks
```

### Split Commits
```
# Original: Large API refactoring with deployment updates
# Becomes:
feat: implement async model serving with connection pooling
perf: reduce inference latency by 40% with caching
fix: handle oom errors in concurrent requests
docs: add api rate limiting documentation
test: add load testing for 1000 concurrent users
mlops: update dockerfile for multi-stage builds

# Original: Package publishing and ci improvements
# Becomes:
mlops: add pypi publishing workflow
test: add integration tests for all api endpoints
docs: update readme with installation instructions
fix: resolve import errors in __init__.py
refactor: restructure package for cleaner imports
```

## Options

- `--lint`: Enable ruff style checks and formatting before committing

## Notes

- Requires files to be staged before running
- Reviews diff for optimal commit structure
- Suggests staging strategy for multi-commit scenarios