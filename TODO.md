# topobuilder to-do list

Checklist of what's left to do. Decisions and history are in WORKLOG.md.
Tick items off as they're finished; add new ones as they come up.

## Now: identifiers and numbering

- [x] Choose the plane router prefix: `fa` ("l" is easily misread as "1")
- [x] Fix pod-to-fabric address order in definitions.txt to
      `3fff:2:[spine]:[fabric]::` (matches both templates)
- [x] Rule: no zero padding in IPv4 octets (`10.10.1.1`, not `10.10.01.01`)
- [x] Workloads: deferred to a later, separate script
- [x] Remove or update the old "change list" sections at the end of
      definitions.txt

## Housekeeping

- [x] Install Rust (rustup) — done by user; cargo/rustc 1.100.0
- [x] Convert CRLF to LF in leaf, spine, and plane templates
- [x] Strip IS-IS lines from leaf, spine, and plane templates (saved in
      templates/pod|plane/isis-config.conf for stage 4)
- [x] Move the current full templates to tests/fixtures/ (originals removed)
- [x] `git init` (branch main, .gitignore for target/ and lab/)
- [ ] Add git remote once the hosted repository is created and reorganized

## Stage 1 — FRR configuration generation (Rust)

- [ ] Let the build take a template directory (e.g. `--templates labs/01`),
      so each lab can have its own base config without script changes

- [ ] 1a. Crate skeleton
- [ ] 1a. Sizing: pods (2–32) -> minimum planes, with unit tests
- [ ] 1b. Data model: nodes (name, IDs, loopbacks)
- [ ] 1b. Data model: links (ports, peer, peer port, addresses)
- [ ] 1b. Unit tests against definitions.txt and pod-template.yaml wiring
- [ ] 1c. Minimal minijinja templates: leaf, spine, plane
- [ ] 1c. Render frr.conf for every router
- [ ] 1c. Check: a 5–8 pod build reproduces the current templates
      (apart from agreed fixes)
- [ ] 1c. Document the variables available to templates
- [ ] User review and sign-off on stage 1

## Stage 2 — containerlab YAML generation (separate module)

- [ ] Topology template (minijinja): nodes, groups, links, management network
- [ ] Groups: kind, FRR image, binds for frr.conf, daemons, vtysh.conf
- [ ] Management network: 10.99.0.0/16, 3fff:99:99::/48
- [ ] Check against pod-template.yaml wiring
- [ ] User review and sign-off on stage 2

## Stage 3 — build command and containerlab deploy

- [ ] Single build command calling the config and YAML modules
- [ ] Pull an FRR image
- [ ] Confirm containerlab accepts `eth01`-style interface names
- [ ] Deploy a small topology (2 pods, 80 routers)
- [ ] Check links are up and addresses are correct
- [ ] Try larger sizes; find the host's practical limit
- [ ] User review and sign-off on stage 3

## Stage 4 — routing (second set of scripts)

- [ ] User to specify the three routing protocol options
- [ ] Bring back IS-IS templates (pod and plane); then delete
      templates/pod/ and templates/plane/
- [ ] BGP: AS numbering from definitions.txt, buildable more than one way
      (unique AS per spine vs. one AS for all spines in a pod)
- [ ] (details to be added)

## Later / maybe

- [ ] Workloads script: adds workload hosts for various kinds of tests
      (decide count per leaf, leaf ports eth17–32, numbering from 65 —
      more than 35 per pod overflows 2 digits)
- [ ] 64-port device support
- [ ] Oversubscription other than 1:1
- [ ] Parallel links (fewer than 16 routers per plane)
