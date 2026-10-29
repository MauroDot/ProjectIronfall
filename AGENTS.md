# Project Ironfall agent policy

## Authorization and scope

The current user request defines the task and its permitted effects.
Read-only and planning tasks permit no file, asset, configuration or Git changes.
Proceed with routine work within authorized scope. Explain any necessary action
outside that scope before requesting authorization.

Before writing, read applicable instructions, .editorconfig, relevant source,
Build.cs/Target.cs files, the project descriptor and affected configuration.
Inspect existing Git status when a repository exists.
Preserve unrelated and pre-existing changes.
Make the smallest coherent change; avoid incidental cleanup or migration.

## Authoritative source and assets

Preserve Content, including external actor and object packages.
The reviewed starting set includes 65 external actor packages and two external
object packages. Review additions and removals explicitly.

Retain project/plugin sources, descriptors, licenses, authored scripts,
configuration, SourceArt and Build/resources files.
Review nested ignore rules before excluding paths.
Do not hide a required dependency because it has a binary extension.

Follow existing Unreal naming and .editorconfig conventions.
Use Unreal reflection and object lifetime rules correctly.
Keep generated-header includes last where required.
Never hand-edit generated code.
Review runtime/editor module separation and new module dependencies.
Do not incidentally change engine association, include order or plugin versions.

Blueprint, map and asset edits require task scope covering those assets.
Inspect affected assets and references first.
Do not bulk resave, migrate, rename, move or delete assets without that scope.
Do not save automatic conversion changes during inspection or smoke testing.
Never edit .uasset or .umap bytes using a text editor.

## Editor, MCP and networking

Verify the editor's exact project path before interacting with it.
Do not assume a connected MCP server targets the intended project.
Inspect tool behavior before use.
Read-only tasks permit only verified read-only tools.
Python, console execution, actor/asset writes, saves, editor launch and PIE
require authorization covering their actual effects.

Use a new short-path disposable copy for isolated validation.
Review plugin startup, listeners, external connections and shared writes.
Do not enable MCP auto-start or external integrations incidentally.
Command-line flags do not establish absolute network isolation.

Keep Android File Server and its network functionality disabled for
Windows-first development. Never enable it with an empty token.
Re-enablement requires separate review and fresh private credential provisioning.

## Secrets and private configuration

Never print credentials or include their values in commands, reports,
diffs, logs, commits or prompts.
Inspect secret settings by presence/status rather than displaying values.
Do not commit private .codex configuration, Saved state or local credentials.
Do not force-add ignored private files.
Do not rotate, erase or transmit credentials outside authorized scope.
Treat exposed credentials as compromised.

Preserve verified recovery copies even when they contain historical secrets.
Do not sanitize a backup by changing its payload or evidence.
Document exposure without reproducing secret values.

## Git and dependencies

Do not initialize, stage, commit, change remotes, contact remotes or install
Git LFS unless the task authorizes those operations.
Do not change global/system Git configuration.

Never discard unrelated work or use destructive Git operations to resolve
uncertainty. History rewriting or data removal requires explicit scope and
a reviewed recovery path.

When staging is authorized, use explicit paths and inspect the complete staged
file list and diff. Review binary changes separately.
Verify that Unreal packages use LFS and that real payloads are available.
Do not equate pointer files with recoverable assets.

Do not run dependency downloads, plugin installations, upstream signing or CI
workflows as incidental build preparation.
Preserve third-party licenses and review redistribution rights.

## Builds and tests

Use UE 5.8.4 and the documented tested toolchain unless a change is authorized.
Follow docs/DEVELOPMENT.md and inspect the installed build wrappers.
Do not generate IDE project files as an unrequested build prerequisite.

Keep test paths short and inspect projected VisualStudioTools output paths.
Use unique reviewed temp/log locations and audit shared engine outputs.
-NoEngineChanges is not a complete filesystem sandbox.
Stop on blocking failures rather than modifying the engine or original project.

Run checks proportionate to the change.
Record commands, exit codes, warnings, errors and skipped checks.
Distinguish source presence from actual plugin compilation.
Distinguish runtime input injection from hardware keyboard verification.
Do not claim success for unrun tests, missing LFS data or unverified process exit.

## Evidence and recovery

Keep private operational evidence outside the source tree in a new destination.
Record intentional source differences and authoritative integrity checks.
Never overwrite or regenerate verified manifests or previous evidence.
Preserve partial artifacts on failure.

Do not automatically restore over, clean or repair an original project,
snapshot or verified restore copy.
Close task-owned editor processes gracefully and verify actual process exit.
Window closure and shutdown log entries alone do not prove termination.
Report integrity failures, unresolved processes and unexpected external activity.
