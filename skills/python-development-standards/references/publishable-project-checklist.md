# Publishable Python Project Checklist

Use this checklist when a Python project is intended to be installed, built, distributed, or published. Complete applicable items before handoff; report any item that cannot be verified.

## Confirm the Project Shape

- Identify whether the deliverable is a library, application, command-line tool, plugin, or combination.
- Confirm the distribution name, import package name, supported Python versions, build backend, license, and release source of truth from repository evidence.
- Preserve the existing package layout unless changing it is required. Do not impose `src/` layout or flat layout solely by preference.
- Remove placeholder names, descriptions, URLs, authors, examples, and `TODO` markers from publishable metadata and documentation.
- Do not invent ownership, contact, license, compatibility, performance, or support claims. Ask or omit optional metadata when repository evidence is absent.

## Complete README.md in Chinese

Write headings, explanations, setup instructions, and usage guidance in Chinese. Keep package names, identifiers, commands, code, protocol names, and license identifiers in their native form.

Include the following sections when applicable:

1. Project name and one concise description of its actual purpose.
2. Main capabilities and important limitations.
3. Supported Python version and required system services or native libraries.
4. Installation commands for the published package and, when useful, local development.
5. A minimal quick-start example that runs against the current public API.
6. CLI commands, API entry points, configuration, environment variables, or file formats users need.
7. Development commands for tests, linting, formatting, typing, and building, but only when the project configures them.
8. License and repository, issue tracker, or documentation links that are known and valid.

Apply these quality checks:

- Match every example, option, default, path, and output to the implementation.
- Make the first example the shortest successful path; move advanced usage later.
- Explain destructive commands, credentials, network access, and generated files before users encounter them.
- Use fenced code blocks with correct language tags and keep commands directly runnable from the documented directory.
- Avoid empty sections, duplicate metadata, marketing filler, and badges that are not backed by a working service.

## Complete pyproject.toml

- Use `pyproject.toml` as the primary project and tool configuration. Keep legacy packaging files only when a supported workflow still requires them.
- Define `[build-system]` with `hatchling` as the backend (`requires = ["hatchling"]`, `build-backend = "hatchling.build"`) unless the repository already commits to a different backend. Manage dependencies, the virtual environment, and the lock file with `uv`.
- Complete applicable `[project]` fields: `name`, `version` or `dynamic`, `description`, `readme`, `requires-python`, `license`, `authors`, `dependencies`, `optional-dependencies`, `scripts`, `entry-points`, and `urls`.
- Set `requires-python` to the actual minimum version the code and its dependencies need, verified against the language features used and each dependency's own `requires-python` floor. Do not raise it to the latest available interpreter or to match the developer's local Python opportunistically; a higher floor should follow from a real requirement, not a default bump.
- Keep the distribution name distinct from the import name when they genuinely differ, and document the import users should write.
- Use one version source. Configure dynamic versioning completely when selected; do not declare `dynamic = ["version"]` without a working provider.
- List only runtime requirements in `dependencies`. Put test, lint, documentation, and build tools in the project's established development dependency mechanism.
- Use environment markers and extras for genuinely conditional features. Avoid exact pins in reusable libraries; use tested lower bounds and add upper bounds only for known incompatibilities. Keep application reproducibility in the existing lock file.
- Define CLI entry points through `[project.scripts]` and point them at a callable that returns an appropriate exit result.
- Configure package discovery for the real layout and include required non-Python package data. Include `py.typed` when the package intentionally publishes inline type information.
- Keep formatter, linter, type checker, test, and coverage configuration consistent with the supported Python floor.
- Ensure the referenced README and license files exist with matching case. Ensure project URLs are valid and use the correct repository.
- Parse the final TOML with the current toolchain; do not rely on visual inspection alone.

## Keep Generated Files Out of Git

Ensure `.gitignore` includes at least:

```gitignore
__pycache__/
*.py[cod]
*$py.class
build/
dist/
*.egg-info/
.venv/
.pytest_cache/
.mypy_cache/
.ruff_cache/
.coverage*
htmlcov/
```

- Preserve additional project-specific ignore rules. Do not ignore source, fixtures, lock files, or required package data by broad pattern.
- Inspect tracked files with `git ls-files` and filter for `__pycache__/`, `.pyc`, and `.pyo` before deleting anything.
- If generated bytecode is tracked or was committed previously, add the ignore rules first, then remove only the exact matched cache files and directories from Git and the working tree. Commit that removal normally and verify the tracked-file query returns no matches afterward.
- Remove generated build, test, and coverage artifacts only after resolving their exact paths. Never target the repository root or an unresolved variable with a recursive delete.
- Do not rewrite Git history solely to erase bytecode. Treat exposed secrets as a separate security incident that may require history rewriting and credential rotation.

## Run Post-Change Verification

1. Run the configured formatter check, linter, type checker, and full test suite.
2. Build both source and wheel distributions with the configured build workflow.
3. Run the configured metadata validation, such as `twine check`, when available.
4. Inspect archive contents and exclude caches, tests or docs not intended for distribution, local paths, secrets, and unrelated files.
5. Install the built wheel into a fresh temporary environment and smoke-test the documented import, primary API, and CLI entry points.
6. Confirm the installed package exposes its declared version and required package data.
7. Re-run every README quick-start command that can execute safely in the local environment.
8. Check `git status`, `git diff --check`, ignore behavior, and tracked bytecode one final time.
9. Report the exact commands run, their results, and any skipped check with its reason.

Do not upload a distribution, publish a release, create a tag, or push changes unless the user explicitly requests that external action.
