# 🚚 Shipment Management Form
 
A web-based Shipment Management Form created using HTML, JavaScript, and JSONPowerDB (JPDB) for managing shipment records. Developed in NetBeans.

---

## Table of Contents

- [Objective](#objective)
- [Input Fields](#input-fields)
- [Features & Logic](#features--logic)
  - [On Page Load](#on-page-load)
  - [On Entering Shipment No.](#on-entering-shipment-no)
  - [Validation](#validation)
  - [On Clicking](#on-clicking)
- [Technologies Used](#technologies-used)

---

## Objective

To store and manage shipment details in the `SHIPMENT` table of the `DELIVERY-DB` database using JSONPowerDB REST APIs.

---

## Input Fields

- Shipment No. (Primary Key)  
- Description  
- Source  
- Destination  
- Shipping Date  
- Expected Delivery Date

---

## Features & Logic

### On Page Load

- All fields except **Shipment No.** are disabled.
- Buttons: **[Save]**, **[Update]**, and **[Reset]** are disabled.
- Cursor is focused on **Shipment No.** field.

### On Entering Shipment No.

- **If Shipment No. does not exist in DB:**
  - Enable all fields, **[Save]** and **[Reset]** buttons.

- **If Shipment No. exists:**
  - Fetch and populate all fields.
  - Disable **Shipment No.** field.
  - Enable **[Update]** and **[Reset]** buttons.

### Validation

- No field can be left empty before **saving** or **updating**.

### On Clicking

- **Save**: Adds the record to the database.
- **Update**: Updates the existing record.
- **Reset**: Clears the form and resets to the default state.

---

## Technologies Used

- **Frontend**: HTML5, CSS, JavaScript (Vanilla JS)  
- **Database**: JSONPowerDB  
- **IDE**: NetBeans
