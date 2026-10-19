# Report 1: Project Description

## 1. Project title

**Community Aid Management System**

## 2. Business idea

A community initiative needs an information system to organise assistance provided to households in need. The proposed system maintains household records, tracks aid requests, manages available aid items, and records distributions handled by volunteers.

This is a proposed scenario for the assignment rather than a claim about a particular organisation.

## 3. Problem statement

The initiative relies on paper records and scattered messages to manage household information, aid requests, and distributions. This makes it difficult to track pending requests, check available stock, and confirm which households have received assistance. Duplicate records, distribution errors, and delays may occur.

The initiative needs a centralised system to organise this information and maintain a clear record of each distribution.

## 4. Purpose

The system aims to help the team monitor request progress, reduce duplicate records, maintain stock records, and document the items and quantities delivered by each responsible volunteer. Eligibility and priority decisions remain the responsibility of authorised staff.

## 5. Project scope

### In-scope

- Register households and update their basic contact information and member counts.
- Record aid requests and track approval, rejection, or cancellation.
- Maintain aid item records and available stock quantities.
- Maintain volunteer records and active status.
- Create distributions for approved requests and assign a responsible active volunteer.
- Record the items and quantities included in each distribution.
- Confirm delivery and update stock quantities accordingly.

### Out-of-scope

- Financial donations, bank transfers, and online payments.
- Purchasing aid items and managing suppliers.
- Live location tracking and delivery route planning.
- Automated eligibility or priority decisions.
- Storage of identity document images or sensitive medical information.
- Development of a working application or implementation of a SQL database.

## 6. Main classes and responsibilities

| Class | Responsibility |
|---|---|
| Household | Maintains the household contact person, phone number, area, and number of members. |
| AidRequest | Records a household's need and tracks the review status of its request. |
| AidItem | Represents an aid item, its unit of measurement, and available stock quantity. |
| Volunteer | Maintains details and active status of volunteers responsible for delivery. |
| Distribution | Records a planned or completed delivery for an approved request and its responsible volunteer. |
| DistributionLine | Specifies one aid item and its quantity within a distribution. |

## 7. System requirements

| ID | Functional requirement |
|---|---|
| FR1 | Create household records with unique identifiers and positive member counts. |
| FR2 | Record each request against exactly one household, initially as Pending. |
| FR3 | Allow authorised staff to approve or reject Pending requests. |
| FR4 | Maintain item stock and accept positive stock additions. |
| FR5 | Create a distribution for an Approved request with an active volunteer and at least one line. |
| FR6 | Require every distribution line to reference one item and specify a positive quantity. |
| FR7 | Confirm delivery only if all required stock is available; record delivery time and deduct stock once. |
| FR8 | Allow cancellation of a planned distribution without deducting stock. |
| FR9 | Preserve delivered records and prevent changes to their lines. |

The system should provide clear validation messages, restrict review actions to authorised staff, and preserve consistency between deliveries and stock updates. Login and permission classes are outside the simplified domain diagram.

## 8. Assumptions and business rules

- Each entity has a unique, stable identifier. A household ID identifies a record; it does not automatically prove that two records represent different real-world households. Staff check possible duplicates during registration.
- A request may be fulfilled through several distributions. This model records needs in free text; staff determine whether those needs have been fully met. Automatic fulfilment calculation is excluded.
- Quantities use whole units. For example, bulk food can be recorded as standard bags rather than fractional quantities.
- Stock is deducted when delivery is confirmed. Planned distributions do not reserve stock, so availability must be checked again at confirmation.
- Delivery confirmation must aggregate all line quantities for each item, validate all stock, then apply all deductions and the status change as one indivisible operation.
- Records referenced by completed deliveries are retained. Composition expresses ownership of distribution lines, not permission to erase delivered history.

## 9. Example scenario

A household requests food and hygiene supplies. Staff approve the request and create a distribution assigned to an active volunteer. It contains two lines: two food baskets and one hygiene kit. When delivery is confirmed, the system checks stock, deducts the quantities once, records the delivery time, and marks the distribution Delivered. Additional assistance can be recorded in a later distribution for the same request.
