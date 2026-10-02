# 🚚 SwiftShip Tracker

### Salesforce Parcel Booking & Tracking System with Agentforce

SwiftShip Tracker is a Salesforce-based parcel booking and tracking application designed to manage parcel information, delivery status, sender and receiver details, and delivery locations.

The project combines **Salesforce custom objects, Lightning App, Flows, Apex automation, Batch Apex, Scheduled Apex, and Agentforce** to provide an end-to-end parcel tracking solution.

---

## 📌 Project Overview

SwiftShip Tracker helps organizations manage parcel deliveries from booking to final delivery.

The system allows users to:

* Create and manage parcel records
* Maintain sender and receiver information
* Track parcel delivery status
* Store delivery location information
* Automatically validate parcel records
* Send notifications when parcel status changes
* Identify overdue parcels
* Provide parcel tracking information through an **Agentforce tracking agent**
* View delivery information through Salesforce reports and dashboards

---

## 🎯 Objectives

The main objectives of SwiftShip Tracker are:

1. To develop a centralized parcel management system using Salesforce.
2. To maintain sender, receiver, parcel, and delivery information.
3. To automate parcel validation and status-change notifications.
4. To identify overdue parcels using Batch Apex and Scheduled Apex.
5. To provide users with quick parcel tracking through Agentforce.
6. To visualize parcel and delivery information using Salesforce reports and dashboards.

---

## 🛠️ Technologies Used

| Technology           | Purpose                                 |
| -------------------- | --------------------------------------- |
| Salesforce           | CRM and application platform            |
| Apex                 | Business logic and automation           |
| Apex Triggers        | Parcel validation and status automation |
| Batch Apex           | Processing overdue parcels              |
| Scheduled Apex       | Scheduling overdue parcel processing    |
| Salesforce Flow      | Parcel tracking information generation  |
| Agentforce           | AI-powered parcel tracking assistant    |
| Lightning App        | User interface                          |
| SOQL                 | Salesforce data querying                |
| Custom Objects       | Data management                         |
| Reports & Dashboards | Data visualization                      |
| GitHub               | Source code and project documentation   |

---

## 🏗️ Salesforce Architecture

The project consists of the following major Salesforce components:

### Custom Objects

* **Parcel__c**
* **Delivery__c**
* **Sender__c**
* **Receiver__c**

### Automation

* Parcel Trigger
* Parcel Trigger Handler
* Overdue Parcel Batch
* Scheduled Apex
* Parcel Details Flow

### User Interface

* SwiftShip Tracker Lightning App
* Custom object tabs
* Salesforce Reports
* Salesforce Dashboard

### AI

* Agentforce Parcel Tracking Agent
* Parcel Tracking Flow Action

---

## 🗃️ Data Model

### Parcel__c

The `Parcel__c` object stores the main parcel information.

Important fields:

* `Parcel_ID__c` – Auto-generated parcel ID
* `Status__c` – Current parcel status
* `Weight__c` – Parcel weight
* `Estimated_Delivery_Date__c` – Expected delivery date
* `Sender__c` – Lookup to Sender

### Delivery__c

The `Delivery__c` object stores delivery and tracking information.

Important fields:

* `Current_Location__c` – Current delivery location
* `Estimated_Delivery__c` – Estimated delivery information
* `Sender__c` – Lookup to Sender
* `Parcel__c` – Lookup to Parcel

### Sender__c

Stores sender information.

Important fields:

* `Sender_Address__c`
* `Sender_Contact__c`
* `Sender_Email__c`

### Receiver__c

Stores receiver information.

Important fields:

* `Receiver_Address__c`
* `Receiver_Contact__c`
* `Receiver_Email__c`
* `Sender__c`
* `Parcel__c`

---

## 📊 Parcel Status

A parcel can move through the following statuses:

```text
Booked
   ↓
In Transit
   ↓
Out for Delivery
   ↓
Delivered
```

The current status of each parcel can be maintained and tracked within Salesforce.

---

## ⚙️ Key Features

### 1. Parcel Management

Users can create and manage parcel records containing:

* Parcel ID
* Parcel weight
* Parcel status
* Estimated delivery date
* Sender information

### 2. Sender & Receiver Management

The application maintains separate sender and receiver information and associates them with parcels.

### 3. Delivery Tracking

Delivery records store the current location and estimated delivery information of parcels.

### 4. Apex Trigger Automation

`ParcelTrigger` and `ParcelTriggerHandler` are used to implement parcel-related business logic.

The automation includes:

* Parcel validation
* Status-change processing
* Status-change email notifications

The trigger handler approach keeps the trigger logic organized and maintainable.

### 5. Overdue Parcel Processing

The `OverdueParcelBatch` class uses **Batch Apex** to process overdue parcels.

The class also implements **Schedulable**, allowing the overdue-parcel processing job to be scheduled automatically.

### 6. Parcel Details Flow

The `Parcel_Details` Flow is an **Auto-Launched Flow**.

It accepts:

```text
Ids
```

as an input containing the Parcel ID and produces:

```text
Output
```

containing the parcel tracking information.

This Flow is also used as an action for the Agentforce tracking agent.

### 7. Agentforce Tracking Agent

SwiftShip Tracker includes an Agentforce agent that can help users retrieve parcel tracking information.

The agent can use the Parcel Details Flow to obtain the relevant parcel information.

Example interaction:

```text
User:
Track parcel P-001

Agent:
Parcel P-001 is currently In Transit.
Estimated delivery: 5 October 2026.
```

The exact response depends on the parcel data available in Salesforce.

### 8. Reports & Dashboard

Salesforce reports and dashboards provide a visual overview of parcel operations.

Possible insights include:

* Total parcels
* Parcel status distribution
* Delivered parcels
* Parcels in transit
* Out-for-delivery parcels
* Overdue parcels
* Delivery information

---

## 🧪 Testing

The project includes the `SwiftShipTests` Apex test class.

Tests can be executed using:

```bash
sf apex run test --target-org swiftship --code-coverage --result-format human --wait 10
```

The test execution verifies the functionality of the Apex automation and reports code coverage.

---

## 🚀 Deployment

### Prerequisites

Make sure the following are installed:

* Salesforce CLI
* Salesforce Developer Org or suitable Salesforce environment
* Git
* GitHub account

### 1. Login to Salesforce

```bash
sf org login web --alias swiftship
```

### 2. Deploy the Salesforce source

```bash
sf project deploy start --source-dir force-app --target-org swiftship
```

### 3. Run Apex Tests

```bash
sf apex run test --target-org swiftship --code-coverage --result-format human --wait 10
```

### 4. Complete Salesforce Setup

Some configuration must be completed manually through Salesforce Setup.

Refer to:

```text
docs/manual-steps.md
```

for instructions related to:

* Prompt Template
* Agentforce Agent
* Reports
* Dashboard
* Other UI-only configuration

---

## 📁 Repository Structure

```text
SHIFT-SHIP-TRACKER/
│
├── force-app/
│   └── main/
│       └── default/
│           ├── applications/
│           ├── classes/
│           ├── flows/
│           ├── objects/
│           ├── permissionsets/
│           ├── tabs/
│           └── triggers/
│
├── docs/
│   ├── manual-steps.md
│   ├── phase documentation
│   ├── screenshots
│   ├── project report
│   └── project templates
│
├── scripts/
│   └── build-report.js
│
├── README.md
└── sfdx-project.json
```

---

## 📚 Documentation

Detailed project documentation is available in the `docs/` folder.

It includes:

* Phase-wise project documentation
* Manual Salesforce configuration steps
* Project report
* Screenshots
* Agentforce configuration
* Reports and dashboard documentation

---

## 📸 Project Screenshots

Screenshots demonstrating the project implementation are available in the `docs/` folder.

The documentation includes screenshots of:

* SwiftShip Tracker Lightning App
* Parcel records
* Sender and Receiver records
* Delivery tracking
* Salesforce Flow
* Apex automation
* Agentforce tracking agent
* Reports
* Dashboard

---

## 🔐 Permissions

The project includes the:

**Swift_Ship Permission Set**

The permission set provides the required access to the SwiftShip Tracker custom objects and their fields.

---

## 💡 Project Highlights

* Salesforce custom application development
* Custom data model
* Apex Trigger and Handler architecture
* Batch Apex
* Scheduled Apex
* Salesforce Flow automation
* Agentforce integration
* Parcel tracking functionality
* Reports and dashboards
* Apex unit testing
* Salesforce CLI deployment
* GitHub-based project management

---

## 👩‍💻 Developer

**Dheepika Selvam**

B.Tech Information Technology

Interested in:

* Salesforce Development
* Data Science
* Artificial Intelligence
* Data Analytics
* Python
* SQL
* Data Visualization

---

## 📅 Project Submission

**Project:** SwiftShip Tracker
**Platform:** Salesforce
**Project Type:** Salesforce Developer Project
**Submission Deadline:** 3 October 2026

---

## ⭐ Conclusion

SwiftShip Tracker demonstrates how Salesforce can be used to build an end-to-end parcel management and tracking solution by combining declarative tools such as **Flow and Lightning Apps** with programmatic technologies such as **Apex, Batch Apex, and Scheduled Apex**, along with **Agentforce** for AI-powered parcel tracking.

The project provides a structured foundation for managing parcel operations while demonstrating practical Salesforce development and automation capabilities.
