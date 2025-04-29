<img width="960" alt="Login2Xplore" src="https://github.com/user-attachments/assets/4141c3a0-e598-4e75-9b6d-af8896359163" />
# 🚚 Shipment Management Form

A web-based Shipment Management Form created using **HTML**, **JavaScript**, and **JSONPowerDB** (JPDB) for managing shipment records. Developed in **NetBeans**.

## 📌 Objective

To store and manage shipment details in the `SHIPMENT` table of the `DELIVERY-DB` database using JSONPowerDB REST APIs.

---

## 🧾 Input Fields

- **Shipment No.** (Primary Key)
- **Description**
- **Source**
- **Destination**
- **Shipping Date**
- **Expected Delivery Date**

---

## 🧠 Features & Logic

- On **page load**:
  - All fields except **Shipment No.** are disabled.
  - Buttons: [Save], [Update], and [Reset] are disabled.
  - Cursor is focused on **Shipment No.**

- On **entering Shipment No.**:
  - If Shipment No. **does not exist** in DB:
    - Enable all fields, [Save] and [Reset] buttons.
    - <img width="960" alt="Login2Xplore1" src="https://github.com/user-attachments/assets/6d1ae8a4-8b05-4045-a2a7-3aae367a2ce5" />

  - If Shipment No. **exists**:
    - Fetch and populate all fields.
    - Disable **Shipment No.** field.
    - Enable [Update] and [Reset] buttons.
    - <img width="960" alt="Login2Xplore" src="https://github.com/user-attachments/assets/f4f5d09b-8dd9-46e3-be2f-70ee041eed93" />


- **Validation**:
  - No field can be empty before saving or updating.
  - <img width="960" alt="Login2Xplore3" src="https://github.com/user-attachments/assets/54e74e9a-0cf6-4258-897b-1149c424d5e6" />


- On clicking
  - **Save**: Adds the record to the DB.
  - **Update**: Updates the existing record.
  - **Reset**: Clears form and resets to default state.

## 🛠️ Technologies Used

- **Frontend**: HTML5, CSS, JavaScript (Vanilla JS)
- **Database**: JSONPowerDB
- <img width="960" alt="Login2Xplore2" src="https://github.com/user-attachments/assets/4871766e-28ab-4431-995a-357d1370a47f" />
- **IDE**: NetBeans
- <img width="960" alt="Login2Xplore4" src="https://github.com/user-attachments/assets/769fe8ea-9c40-4502-8a27-bbd2929b5d94" />


