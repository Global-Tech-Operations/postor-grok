---
name: account-work
description: Create Postor projects and tasks, update tasks, and manage Almacén folders within the connected user's permissions.
---

Consult membership, permissions and feature availability when needed. Use IDs
returned by tools for the connected company. Read the affected resource before
updating tasks or folders, or deleting a folder. For project stages and tender
associations, target a stage in the same project. Assign only a known active
member of the same company; never infer a collaborator's ID.

Each operation is a separate named tool with its own input schema, OAuth scope
and safety annotations. Invoke the requested action directly: create_project,
add_licitacion_to_project and create_project_task for project work;
create_storage_folder, update_storage_folder and delete_storage_folder for
Almacén. update_project_task changes an existing task. Supply
params, query and body exactly as that tool's schema requires. requestKey and
confirmed are top-level fields. Never select an operation through a generic
executor, invent a tool or infer that one action authorizes another.

Operate only within the user's stated task. Before destructive changes or
changing a task or folder, obtain specific confirmation of resource, changes
and consequences. Then pass `confirmed: true`. That argument
is a declaration of human consent, not permission to invent consent. Broad
account access does not authorize arbitrary or bulk cleanup.

Give each write a unique `requestKey`; reuse it for the identical action if its
response is lost. The replay window is 24 hours. Never automatically use a new
key after `ACTION_STATE_UNKNOWN`: inspect the resource first and report the
uncertainty. Do not claim success if the tool returned an error or partial data.

`ACTION_STATE_UNKNOWN` is a stop condition, including on the first attempt:
the server may have committed the write even if its response was lost. Inspect
the resource and explain uncertainty. Authentication recovery may retry a read
once, but never authorizes an automatic replay or new-key retry of a write.
Use `structuredContent` as the machine-readable result; text contains the same
JSON for compatibility. Honor `truncatedFields` and follow pagination instead
of treating omitted content as absent. Use only returned Postor panel links.

For the user's own document analysis in Grok Build, obtain originals with
list_licitacion_documents and get_licitacion_document and use the host's file
capabilities. For document pages omit query.limit/query.extractedLimit (10 by
default), or use integers from 1 to 25. Follow nextOffset/nextExtractedOffset
until null when all files are requested. If INVALID_ARGUMENTS names either
limit, correct that read to 25 or omit the field and continue; do not reconnect
an active account. Do not start OCR or Postor analysis jobs as a fallback.

This plugin publishes 32 independently named operations. For projects it can
list and read projects, create a project, associate a tender, and list, create
or update tasks. For Almacén it can list/read, create, rename and delete folders.
Other platform actions are outside this plugin: deleting projects, moving
resources, editing stages, posting messages, sharing folders, configuring alerts,
accessing private file bytes, and starting or reading Postor analysis jobs.
Do not invent tools for these actions or ask to reconnect to enable them.
Do not claim to have read a private file whose metadata you listed.

Membership, feature, role and quota refusals are normal results. Explain them
without checkout, promotions, pricing or promises to bypass permissions. Existing
Postor quotas apply and there is no Grok Build-specific surcharge.
