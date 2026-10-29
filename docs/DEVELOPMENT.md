# Project Ironfall development and recovery

## Validated environment

- Unreal Engine 5.8.4, changelist 58902052, compatible changelist 55116800.
- Tested installed engine location: F:\UE_5.8.
- Recorded Visual Studio Enterprise 2026 version: 18.11.2.
- Successful builds used MSVC toolchain 14.50.35739 from directory
  E:\VisualStudio\VC\Tools\MSVC\14.50.35717.
- Recorded compiler file version: 19.50.35739.
- Windows SDK: 10.0.22621.0.
- Engine-bundled DotNet: 10.0.

These are tested versions, not a compatibility guarantee for other versions.
The engine and toolchain are external prerequisites.
The descriptor's EngineAssociation GUID is machine-specific.
Use the reviewed engine executable/build path explicitly; do not silently
rewrite association or upgrade the project.

The exact engine distribution must provide the enabled engine plugins,
including GameplayStateTree, ModelingToolsEditorMode, MCPClientToolset,
ModelContextProtocol and AllToolsets and their dependencies.
Do not assume another engine installation contains these components.
Do not copy engine plugin payloads into this repository automatically.

## Authoritative inputs

Retain the descriptor, Source, reviewed Config, all Content, required project
plugin sources/descriptors, licenses, documentation and authored build resources.
Preserve all external actor/object packages, including the reviewed starting
65 external actor packages and two external object packages.
Do not broadly exclude SourceArt, Build or built-data assets.

The original source proof contains 302 files. It includes private local
.codex/config.toml and a UI-only editor default.
Excluding those two reviewed files leaves 300 existing candidate files.
New policy files and deliberate configuration changes create a different
prospective baseline. Review exact paths rather than assuming a fixed count.

VisualStudioTools 2.8 is project-local. Its VisualStudioTools and
VisualStudioBlueprintDebuggerHelper Editor modules compiled and linked from
source during the clean Editor build.
Retain its MIT license, Source, descriptor, Config, Docs/images, build.proj,
Scripts/SignDetached.proj, Scripts/packages.config and other authored files.
No precompiled-only project module was identified.

The upstream packaging/signing workflow references MicroBuild.Core 0.4.1.
That workflow was not required for the successful Editor/Game target builds.
Do not run its restore, signing, cleanup or CI steps as normal build preparation.

## Windows-first Android defaults

Android File Server is disabled explicitly in the descriptor and configuration.
Its network functionality is disabled and its credential is absent from shared
configuration.
Do not re-enable it without reviewed private provisioning of a fresh nonempty
credential and assessment of any older deployed installation.
Ignored files are not automatically secure and are not automatically loaded
as Unreal configuration.

## Fresh source rebuild

Use a new short disposable checkout/copy.
Never overwrite, clean or build inside a protected snapshot, previous test
copy or original project merely to validate recoverability.
Start without generated project/plugin output.
Review nested exclusions and required binary dependencies first.
When restoring from Git, obtain real LFS payloads before building.

The original long test path produced UBT action paths of 261-268 characters.
G:\IFBuild\ProjectIronfall reduced the longest generated build path to 199.
Use similarly short paths and inspect projected plugin paths before execution.

Close conflicting editor, Live Coding and build processes.
Inspect the installed Build.bat and UBT write paths before executing.
Use fresh process-local TMP/TEMP and log locations.
Stop if protected or existing engine intermediate files would be replaced
without specific authorization.

From the fresh disposable project directory, the direct target form is:

```powershell
$Engine = 'F:\UE_5.8'
$Project = (Resolve-Path '.\ProjectIronfall.uproject').Path
$Flags = @(
    '-NoEngineChanges', '-NoUBTMakefiles', '-NoUBA',
    '-NoXGE', '-NoFASTBuild', '-NoSNDBS'
)

& "$Engine\Engine\Build\BatchFiles\Build.bat" `
    ProjectIronfallEditor Win64 Development "-Project=$Project" @Flags
$editorExitCode = $LASTEXITCODE
if ($editorExitCode -ne 0) {
    throw "Editor build failed with exit code $editorExitCode."
}

& "$Engine\Engine\Build\BatchFiles\Build.bat" `
    ProjectIronfall Win64 Development "-Project=$Project" @Flags
$gameExitCode = $LASTEXITCODE
if ($gameExitCode -ne 0) {
    throw "Game build failed with exit code $gameExitCode."
}
```

Add a unique reviewed -Log= location for each invocation.
These commands require an authorized build task and a completed write-path audit;
they are not instructions to build automatically while reading this document.

Direct target arguments do not request IDE project-file generation.
Build.bat can rebuild UBT depending on installed inputs.
The tested installation skipped that branch because its UBT DLL existed and
BuildUBT.bat was absent.
UBT still uses shared engine run bookkeeping and user-profile trace output.
-NoEngineChanges guards existing engine action outputs; it is not a sandbox.
Recorded executor flags do not establish network isolation.

## Historical validation results and limitations

The results in this section predate B4-B sanitization. The new B4-B configuration
has not been built or launched; the example above was not executed during B4-B.

Independent clean Editor and Game builds exited 0, taking 201.58 and
174.78 seconds respectively.
The current targets use BuildSettingsVersion.V7 and inherited Unreal5_6
include order. Upgrade notices were recorded; include order was not changed.

A disposable UE 5.8.4 Editor loaded /Game/ThirdPerson/Lvl_ThirdPerson.
The expected ThirdPerson pawn, controller, game mode, camera and camera boom
were found. Bounded Enhanced Input injection verified movement, jump and look.
Sustained physical keyboard movement/jump remains unverified.
No source assets were saved.

Eventual editor and Trace Server termination was confirmed.
The exact editor exit time and exit code were not captured.

MCP and AFS were disabled for the gameplay smoke test.
External HTTPS, Trace listeners and shared trace writes still occurred.
The session also recorded a prolonged shader-worker delay and audio warnings.
Do not claim absolute network isolation or full MCP validation.
MCP validation remains deferred.

## Recovery and source control

Preserve full backup payloads, restore copies, manifests and evidence unchanged
outside Git with restricted access. They may contain historical secrets.
Keep private recovery locations and operational evidence in operator records.

Use a new destination for restoration drills.
Verify paths, counts, hashes and dependencies before clean target builds.
Review launch safety separately before editor or PIE testing.
Never restore over the original project as an automatic repair.

The repository requires Git LFS for .uasset and .umap.
Text attributes normalize supported source/configuration files to LF, with
Windows batch scripts using CRLF.
Original raw text hashes may therefore differ after normalization.
Preserve historical manifests and establish a new authorized baseline;
do not regenerate old evidence to match a checkout.

Asset provenance and engine-plugin redistribution review remain gates before
remote publication. Git/LFS configuration and remote recovery have not yet
been validated.
Successful local builds do not prove remote recoverability.
A separately authorized clean clone, LFS retrieval and build drill is required
before claiming GitHub/Git LFS recovery works.
