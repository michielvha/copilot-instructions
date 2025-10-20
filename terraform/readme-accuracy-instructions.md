# README Accuracy Review & Minimal Update Instructions

## Objective

Review the entire codebase and the existing README.md to ensure the README accurately reflects the current Terraform module state. Propose and apply ONLY the minimal necessary changes to bring it up to date. If the README is already accurate, make no changes.

## Hard Constraints (Do NOT violate these)

**IMPORTANT:** You may modify ONLY `README.md`. Do not create, delete, or edit any other files. 

- **YOU ARE NOT ALLOWED TO CHANGE ANY FILE OTHER THAN README.md**
- Preserve the current overall structure, section ordering, and intent of the README
- Make the smallest set of textual/formatting changes needed for accuracy and clarity
- Do NOT introduce speculative or undocumented features
- Do NOT add marketing fluff, badges, or sections not already present unless essential for factual correction
- Reformat Markdown only where it is objectively broken (e.g., incorrect headings, code fences, list indentation, inconsistent backticks) or where small adjustments improve readability without altering meaning
- If no changes are required, explicitly output: **"No README changes needed."** and stop

## Scope of Verification (Systematically check these against the repository)

For each item below, compare what is stated in README.md vs. what actually exists in the repo:

- Project purpose / high-level description
- Module features and capabilities
- Terraform version requirements (check `00-version.tf` or similar version files)
- Provider requirements (AWS, Kubernetes versions from `00-version.tf`)
- Input variables (compare README with `98-variables.tf` or other variable files)
- Output values (compare README with `99-output.tf` or other output files)
- Resource listings (validate against actual `.tf` files in root: `02-cluster.tf`, `03-nodegroup.tf`, `04-addon.tf`, `05-access.tf`, `06-iam-autoscaling.tf`, `10-iam-eso.tf`, `11-iam-alb.tf`, `12-iam-cas.tf`, `13-iam-jro.tf`, `20-argocd.tf`, `21-dns-resolver.tf`)
- Usage examples (ensure HCL syntax is correct and references valid variables)
- Configuration options (ArgoCD, External Secrets, ALB Controller, Cluster Autoscaler, JFrog, DNS Resolver, CrowdStrike)
- Default values for variables
- File structure and organization
- Example configurations in `examples.d/` directory

## Evidence Sources

Use (non-destructively) the following files to ground truth:

- `98-variables.tf` (all input variables, types, defaults, descriptions)
- `99-output.tf` (all module outputs)
- `00-version.tf` (Terraform and provider version requirements)
- `02-cluster.tf` through `21-dns-resolver.tf` (actual resources created)
- `examples.d/main.tf` (example usage if present)
- `gitversion.yml` (versioning configuration if relevant)

## Change Decision Rules

Propose a change ONLY if one of these is true:

1. README claims a variable/output/resource that doesn't exist in the Terraform files
2. README omits a clearly essential variable or feature that exists in the code
3. A variable name, type, default value, or description differs between README and `98-variables.tf`
4. An output differs between README and `99-output.tf`
5. Provider or Terraform version requirements are incorrect
6. HCL code examples contain syntax errors or reference non-existent variables
7. Resource listings are outdated or incomplete
8. Formatting obscures readability (mis-nested lists, broken code fences, ambiguous inline code vs prose)

## Explicitly DO NOT

- Add new feature ideas not present in the code
- Rewrite stylistically for preference alone
- Expand sections with tangential info
- Introduce unverified claims about performance or capabilities
- Adjust license terms
- Add badges, CI/CD status indicators, or contributor graphs unless they already exist
- If no changes: don't make any modifications to the file

## Process You Must Follow (Sequential)

1. Read all Terraform `.tf` files to build an internal fact map of the module
2. Parse current README.md into sections (record order; reuse it)
3. For each section, verify against actual Terraform code:
   - Variables section → `98-variables.tf`
   - Outputs section → `99-output.tf`
   - Requirements → `00-version.tf`
   - Resources → individual `.tf` files
   - Usage examples → validate HCL syntax and variable references
4. Mark each section: accurate / outdated / missing detail / formatting issue
5. Prepare minimal edits; reject any that are not strictly necessary
6. Ensure internal links, code fences, table formatting, and inline code consistency
7. **Verify you have NOT modified any file other than README.md**
8. If changes made, provide a detailed summary of what changed and why

## Quality Checklist Before Completion

- [ ] No Terraform files (.tf) touched
- [ ] No other files created, deleted, or modified
- [ ] Section order preserved
- [ ] No invented features, variables, or resources
- [ ] All modified claims verifiable in Terraform code
- [ ] HCL syntax in examples is valid
- [ ] Variable types and defaults match `98-variables.tf`
- [ ] Output descriptions match `99-output.tf`
- [ ] Markdown syntax valid (tables, code fences, lists)

## Failure Handling

If you cannot confidently verify a claim from the Terraform code, leave it unchanged unless clearly false. Do not guess or invent details.
