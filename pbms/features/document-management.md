---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Document Management

OpenG2P platform allows multiple options for managing registrant documents, evidence documents, entitlement vouchers, accounts payable files, etc. Program administrators can later view these documents from the program view for assessment and verification. These are the currently supported document management options:

1. AWS S3 object store
2. MinIO object store
3. Private filesystem

Users can configure multiple document stores from a single view. The diagram below shows three document stores using the Amazon S3 object-store.

<figure><img src="../../.gitbook/assets/document-storage-options.png" alt=""><figcaption></figcaption></figure>

All the users of the OpenG2P platform such as System Administrators, Program Administrators, Finance Officers, and Social workers can upload/edit/delete these documents based on their [role-based access](administration/role-based-access-control/).

### Document files

Each document file is assigned a Universally Unique ID (UUID) known as S\_lug\_ by the system. Information about document store, file UUID, size, and type are available from a single view.

<figure><img src="../../.gitbook/assets/document-files.png" alt=""><figcaption></figcaption></figure>

### Document tags

The platform users can define unique tags and associate them with their upload files.

<figure><img src="../../.gitbook/assets/document-tags.png" alt=""><figcaption></figcaption></figure>
