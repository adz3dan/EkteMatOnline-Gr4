# Ekte Mat Online — Requirements overview

**INFO212 — Obligatory Assignment 4**  
**Status:** Initial plan for group review (not a record of completed features)  
**Sources:** `INFO212_Oblig4_EkteMat_Claude_Code.pdf` (minimum requirements) and selected interviews/process notes in `Lab_EkteMat_DataPack_STUDENTS.zip` (stakeholder needs).

## 1. Project goal

Ekte Mat AS is a fictional catering business in Bergen. Today, orders arrive by email or telephone and are managed manually in Excel. We will develop a **working first version** of *Ekte Mat Online*: a website where customers can browse food and place orders, plus an admin panel where staff can manage the menu, orders and questions.

**Prioritisation:** Implement the nine minimum requirements (C1–C5 and A1–A4) before considering optional features. The stakeholder needs below explain *why* each feature is useful; they do not create extra mandatory scope.

## 2. Customer site — minimum requirements

| ID | Feature / what the system must do | Stakeholder need | Simple acceptance check |
|---|---|---|---|
| **C1** | **Menu by event:** Show published food items as cards, grouped by event category (birthday, confirmation, wedding, conference, julebord, etc.). Each card shows an image, price, minimum quantity and allergens. | Customers need to view menus and prices without emailing the business. *Source: `interview_Ingrid_owner.txt`.* | Can a customer find food for an event and see all required information? Are unpublished items hidden? |
| **C2** | **Shopping cart:** Add, change or remove food items; show estimated total cost; reject quantities below each item's minimum. | Customers should be able to prepare an order themselves. *Source: `interview_Ingrid_owner.txt`.* | Does the total update, and are quantities below the minimum rejected? |
| **C3** | **Place order:** Customer registers or logs in, then submits an order with event date, number of guests, delivery address and allergy/dietary notes **per guest group**. **No payment solution is required.** | Replace manual email/phone orders and avoid losing allergy information. *Sources: `interview_Ingrid_owner.txt`, `interview_Sunniva_event_coordinator.txt`.* | Can a logged-in customer submit an order containing the required information? |
| **C4** | **My orders:** A customer can see their own orders, order statuses and payment statuses. | Customers need clear updates instead of waiting for replies. *Sources: `interview_Fjordtek_customer.txt`, `interview_Sunniva_event_coordinator.txt`.* | Can a customer see their orders and statuses, but not another customer's orders? |
| **C5** | **Questions:** A customer can ask a question about a specific order and read the staff's answer. | Inquiries can be missed or delayed when handled through email. *Sources: `interview_Ingrid_owner.txt`, `asis_order_process.md`.* | Can a customer send a question and later see the reply for that order? |

## 3. Admin panel — minimum requirements

| ID | Feature / what the system must do | Stakeholder need | Simple acceptance check |
|---|---|---|---|
| **A1** | **Food items:** Add, edit and remove food items, including name, description, NOK price, minimum order quantity, event categories, allergens, dietary labels and published/unpublished status. | Staff need to update menus as dishes change with the seasons. *Source: `interview_Mateo_head_chef.txt`.* | Can staff create/edit/remove an item and control whether customers see it? |
| **A2** | **Images:** Upload an image for a food item **or** write an instruction for an AI agent/image service to create or edit it. Staff must preview the image before saving it. | Food should be clearly presented on the customer site. *Source: requirement A2 in Oblig 4; this precise image workflow is not specified in the interviews.* | Can staff preview an uploaded or generated image before saving it to a food item? |
| **A3** | **Orders:** List all orders; filter by status and event date; open order details; update order status (`submitted → approved → in preparation → delivered`, or `rejected/cancelled`) and payment status (e.g., `not paid`, `deposit paid`, `invoiced`, `paid`). | Staff need one reliable overview instead of separate emails, Excel sheets and printouts. *Sources: `interview_Sunniva_event_coordinator.txt`, `asis_order_process.md`.* | Can staff filter orders and update both kinds of status? |
| **A4** | **Questions:** Read and answer customer questions about orders. | Staff need to follow up inquiries systematically. *Sources: `interview_Ingrid_owner.txt`, `asis_order_process.md`.* | Can staff open a question, answer it and make that answer visible to the customer? |

## 4. Technical and delivery requirements

- **Backend:** Python with Flask. Use **MVC**, with separate model, view and controller layers. Controllers are Flask routes grouped into blueprints (for example `shop`, `account`, `admin`).
- **Frontend:** HTML/CSS/JavaScript and Jinja2 templates (a separate frontend is also allowed, but not needed for our plan).
- **Storage:** SQLite or JSON may be used temporarily. **Only repository classes in the model layer may access the data store**, so it can later be replaced with Neo4j without changing controllers or views. Neo4j implementation is **not required in Oblig 4** unless the group chooses to combine it with Oblig 5.
- **Test data:** Use synthetic data only. Provide a seed script that creates sample food items, an admin and test customers.
- **Security:** Do not commit Claude API keys or other secrets to GitHub. Restrict customer-specific information to its owner and admin functions to staff.
- **Team workflow:** Use GitHub; **every member must make commits**. Keep a short and accurate `CLAUDE.md`. Use Claude Code **Plan mode** for larger features and commit approved plans to `docs/plans/`.
- **README:** Include instructions to install, seed, run and test the application.
- **Submission:** One PDF report containing group/repository/version details, features and screenshots, design diagrams and a short reflection on whether design helped. Follow the complete submission checklist in the assignment PDF.

## 5. Scope and decisions

**Not required in this assignment:** Online payment integration (Vipps), Fiken integration, automatic reminders, kitchen dashboard, corporate recurring orders and supplier-origin tracking. These appear in the data pack as possible business needs, but are not part of the minimum feature list.

**Team decisions to confirm before implementation:**
1. Use SQLite as temporary storage and Jinja2 templates for the first version?
2. Agree on the folder structure in `docs/architecture.md` and make sure Claude Code follows it.
3. Choose a straightforward staff-access approach for the admin panel. The assignment permits a basic security setup; the team should still avoid exposing admin functions publicly.
4. Review unresolved payment/deposit expectations from stakeholders if planning *extra* features. **Do not add a payment gateway to the minimum version.**

## 6. How the team will use this document

1. Read this overview together and correct anything the team disagrees with.
2. Ask Claude Code to **plan**, not immediately implement, the minimum features using this file and `docs/architecture.md`.
3. Review the plan, save agreed feature plans under `docs/plans/`, then build and test features incrementally.
4. Use the acceptance checks in the tables when reviewing the working application.

> **Note:** This is a deliberately short starting requirements overview, not the full backlog from the optional Claude Cowork lab. The compulsory assignment PDF remains the authority for exact requirements.
