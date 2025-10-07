Absolutely! I’ll create a **full, clean documentation** in Markdown (`DOCUMENTATION.md`) format for your Intellibill project, including:

* Table names
* Field names
* Data types
* Primary keys (PK)
* Foreign keys (FK)
* Relationships
* A simple diagram showing table relationships

Here’s a ready-to-use `DOCUMENTATION.md`:

---

# IntelliBill Database Documentation

## Overview

This database is designed to simulate an IntelliBill claims system. It contains tables for clients, groups, practices, physicians, fee schedules, and claim management (notes, attachments, audit history). All tables include **fake data** for testing purposes.

---

## Table: `client`

| Column                | Data Type | Description                            | Key |
| --------------------- | --------- | -------------------------------------- | --- |
| client_id             | INTEGER   | Unique client identifier               | PK  |
| client_status         | STRING    | Status of the client (Active/Inactive) |     |
| client_taxid          | STRING    | Client Tax ID                          |     |
| client_name           | STRING    | Client Name                            |     |
| client_contact_lnam   | STRING    | Contact Last Name                      |     |
| client_contact_fnam   | STRING    | Contact First Name                     |     |
| client_contact_email  | STRING    | Contact Email                          |     |
| client_contact_number | STRING    | Contact Phone Number                   |     |
| client_addr1          | STRING    | Address line 1                         |     |
| client_addr2          | STRING    | Address line 2                         |     |
| client_city           | STRING    | City                                   |     |
| client_zip            | STRING    | ZIP Code                               |     |
| client_logo           | STRING    | Path to client logo                    |     |

**Relationships:**

* One-to-Many with `group_table` (`client_id`)
* One-to-Many with `practice` (`client_id`)
* One-to-Many with `physician` (`client_id`)

---

## Table: `group_table`

| Column             | Data Type | Description          | Key                     |
| ------------------ | --------- | -------------------- | ----------------------- |
| grp_taxid          | STRING    | Group Tax ID         | PK                      |
| client_id          | INTEGER   | ID of parent client  | FK → `client.client_id` |
| grp_name           | STRING    | Group Name           |                         |
| grp_addr1          | STRING    | Address line 1       |                         |
| grp_addr2          | STRING    | Address line 2       |                         |
| grp_city           | STRING    | City                 |                         |
| grp_st             | STRING    | State                |                         |
| grp_zip            | STRING    | ZIP Code             |                         |
| grp_npi            | STRING    | NPI number           |                         |
| grp_ptan           | STRING    | PTAN                 |                         |
| grp_contact_lnam   | STRING    | Contact Last Name    |                         |
| grp_contact_fnam   | STRING    | Contact First Name   |                         |
| grp_contact_email  | STRING    | Contact Email        |                         |
| grp_contact_number | STRING    | Contact Phone Number |                         |

**Relationships:**

* One-to-Many with `practice` (`grp_taxid`)
* One-to-Many with `physician` (`grp_taxid`)
* One-to-Many with `fee_schedules` (`group_id`)

---

## Table: `practice`

| Column              | Data Type | Description          | Key                          |
| ------------------- | --------- | -------------------- | ---------------------------- |
| prct_id             | INTEGER   | Unique Practice ID   | PK                           |
| client_id           | INTEGER   | Parent client ID     | FK → `client.client_id`      |
| grp_taxid           | STRING    | Parent group Tax ID  | FK → `group_table.grp_taxid` |
| prct_name           | STRING    | Practice Name        |                              |
| prct_addr1          | STRING    | Address line 1       |                              |
| prct_addr2          | STRING    | Address line 2       |                              |
| prct_city           | STRING    | City                 |                              |
| prct_st             | STRING    | State                |                              |
| prct_zip            | STRING    | ZIP Code             |                              |
| prct_npi            | STRING    | NPI number           |                              |
| prct_contact_lnam   | STRING    | Contact Last Name    |                              |
| prct_contact_fnam   | STRING    | Contact First Name   |                              |
| prct_contact_email  | STRING    | Contact Email        |                              |
| prct_contact_number | STRING    | Contact Phone Number |                              |

---

## Table: `physician`

| Column             | Data Type | Description               | Key                          |
| ------------------ | --------- | ------------------------- | ---------------------------- |
| phy_id             | INTEGER   | Unique Physician ID       | PK                           |
| client_id          | INTEGER   | Parent client ID          | FK → `client.client_id`      |
| grp_taxid          | STRING    | Parent group Tax ID       | FK → `group_table.grp_taxid` |
| phy_name           | STRING    | Physician Name            |                              |
| phy_addr1          | STRING    | Address line 1            |                              |
| phy_addr2          | STRING    | Address line 2            |                              |
| phy_city           | STRING    | City                      |                              |
| phy_st             | STRING    | State                     |                              |
| phy_zip            | STRING    | ZIP Code                  |                              |
| phy_npi            | STRING    | NPI Number                |                              |
| phy_taxonomy       | STRING    | Taxonomy code             |                              |
| phy_taxonomy_desc  | STRING    | Taxonomy description      |                              |
| phy_ptan           | STRING    | PTAN                      |                              |
| phy_pecos          | STRING    | PECOS                     |                              |
| phy_lic            | STRING    | License Number            |                              |
| phy_otherid        | STRING    | Other ID                  |                              |
| phy_type           | STRING    | Physician Type (MD/DO/NP) |                              |
| phy_contact_lnam   | STRING    | Contact Last Name         |                              |
| phy_contact_fnam   | STRING    | Contact First Name        |                              |
| phy_contact_email  | STRING    | Contact Email             |                              |
| phy_contact_number | STRING    | Contact Phone Number      |                              |

---

## Table: `fee_schedules`

| Column         | Data Type | Description           | Key                          |
| -------------- | --------- | --------------------- | ---------------------------- |
| fs_id          | INTEGER   | Fee Schedule ID       | PK                           |
| company_id     | INTEGER   | Company ID            |                              |
| group_id       | STRING    | Group Tax ID          | FK → `group_table.grp_taxid` |
| carrier_id     | INTEGER   | Carrier ID            |                              |
| fs_panel_name  | STRING    | Panel Name            |                              |
| fs_proccd      | STRING    | Procedure Code        |                              |
| fs_proccd_desc | STRING    | Procedure Description |                              |
| fs_mod         | STRING    | Modifier              |                              |
| fs_mdcamt      | FLOAT     | Medicare Amount       |                              |
| fs_billamt     | FLOAT     | Billing Amount        |                              |

---

## Table: `claim_audit_history`

| Column            | Data Type | Description                   | Key |
| ----------------- | --------- | ----------------------------- | --- |
| transaction_id    | INTEGER   | Transaction ID                | PK  |
| clm_aud_id        | INTEGER   | Audit ID                      |     |
| clm_aud_mod       | STRING    | Module                        |     |
| clm_aud_queue     | STRING    | Queue Name                    |     |
| clm_aud_cur_owner | STRING    | Current Owner                 |     |
| clm_aud_prv_owner | STRING    | Previous Owner                |     |
| clm_aud_action    | STRING    | Action (Insert/Update/Delete) |     |
| clm_aud_date_time | DATETIME  | Audit Timestamp               |     |
| clm_aud_login     | STRING    | User Login                    |     |

**Relationships:**

* One-to-Many with `claim_notes` (`transaction_id`)
* One-to-Many with `claim_attachments` (`transaction_id`)

---

## Table: `claim_notes`

| Column         | Data Type | Description        | Key                                       |
| -------------- | --------- | ------------------ | ----------------------------------------- |
| notes_table    | INTEGER   | Note ID            | PK                                        |
| transaction_id | INTEGER   | Parent transaction | FK → `claim_audit_history.transaction_id` |
| clm_note_id    | INTEGER   | Claim Note ID      |                                           |
| clm_note_type  | STRING    | Note Type          |                                           |
| clm_note_text  | STRING    | Note Text          |                                           |
| clm_date_time  | DATETIME  | Timestamp          |                                           |
| clm_login      | STRING    | User Login         |                                           |

---

## Table: `claim_attachments`

| Column            | Data Type | Description        | Key                                       |
| ----------------- | --------- | ------------------ | ----------------------------------------- |
| clm_att_id        | INTEGER   | Attachment ID      | PK                                        |
| transaction_id    | INTEGER   | Parent transaction | FK → `claim_audit_history.transaction_id` |
| clm_att_path      | STRING    | File Path          |                                           |
| clm_att_filename  | STRING    | File Name          |                                           |
| clm_att_date_time | DATETIME  | Timestamp          |                                           |
| clm_login         | STRING    | User Login         |                                           |

---

## **Database Relationship Diagram**

```text
client (1) ──< group_table >──< practice
           \                 \
            \                 > physician
             \
              > fee_schedules

claim_audit_history (1) ──< claim_notes
                         └─< claim_attachments
```

* **(1) → <** = One-to-Many relationship
* Arrows indicate foreign key linkage

---
