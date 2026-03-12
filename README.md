# AutoMAYtion2026: ImmyBot Onboarding Handler

The **ImmyBot Onboarding Handler** extends the functionality of Rewst’s **Microsoft: User Onboarding** Crate by introducing advanced ImmyBot-specific options directly into the onboarding process.

By adding additional fields to the onboarding form, this automation can automatically generate your selected ImmyBot installer and attach it to the onboarding ticket. For users receiving pre-deployed hardware, the workflow can instead reassign an existing machine and initiate a maintenance session—ensuring the user is fully prepared on day one.

---

## 1. Installation

This automation assumes the following prerequisites:

- An existing **ImmyBot integration** configured in your Rewst environment
- The **Microsoft: User Onboarding** Crate has already been unpacked
- A supported PSA system is configured  
  - This implementation uses **ConnectWise PSA**, but the workflow can be adapted to other ticketing platforms with minor adjustments

---

### Import Form Bundle

1. Navigate to the **Immy Onboarding Handler** folder.
2. Download the form bundle:  
   `form-019cd2be-c5cc-7733-bf99-83356061dfbc_20260312_145611.bundle.json`
3. In Rewst, go to **Forms**.
4. Select **Import Bundle**.
5. Drag and drop the downloaded form bundle.
6. Review the objects to be imported and confirm the selection.

> 📸 *Screenshots of the form import process can be added here.*

---

### Import Workflow Bundle

1. Navigate to the **Immy Onboarding Handler** folder.
2. Download the workflow bundle:  
   `workflow-019afff1-45af-7079-85c8-9d09a62a4018_20260312_150235.bundle.json`
3. In Rewst, go to **Workflows**.
4. Select **Import Bundle**.
5. Drag and drop the downloaded workflow bundle.
6. Review the objects to be imported and confirm the selection.

> 📸 *Screenshots of the workflow import process can be added here.*

---

### Configure Form Trigger

1. Open the **Microsoft: User Onboarding** workflow in the Workflow Builder.
2. Create a new **Form Trigger**.
3. Assign organization overrides for:
   - **ConnectWise PSA**
   - **ImmyBot**
4. Select the newly imported onboarding form.

---

### Configure Completion Handler

1. While still in the **Microsoft: User Onboarding** workflow:
   - Create a new **Completion Handler**.
2. Select the newly imported **Immy Onboarding Handler** workflow.
3. Configure it to run upon **successful onboarding completion**.

---

## 2. Usage

To use this workflow:

1. Open the new onboarding form for the desired client.
2. Complete the standard onboarding fields.
3. Navigate to:  
   **Customize Advanced Options → Advanced – ImmyBot Options**

---

### Prepare an Existing Computer

- Select **Use Existing Computer**
- Choose the appropriate **ImmyBot computer** and **user** from the dropdown menus

This will:

- Assign the selected user to the machine in ImmyBot
- Start a maintenance session on the device
- Update the onboarding ticket with a link to the maintenance session page

---

### Prepare a New Computer

- Select **New Immy Installer**
- Choose your preferred **ImmyBot installer format**

Available options:

- **OOBE (.ppkg)**  
  - Updates the ticket notes with a client-specific provisioning package download link
- **Post-OOBE (.exe)**  
  - Updates the ticket notes with a client-specific executable download link
- **Post-OOBE (.ps1)**  
  - Attaches a PowerShell script directly to the ticket

> 📸 *Screenshots of installer selection and ticket updates can be added here.*

---

By leveraging this completion handler, technicians can onboard users and begin hardware preparation from a single submission—streamlining both identity and device readiness workflows.

---

## 3. Improvement Ideas

### ImmyBot Azure Sync After M365 Onboarding

Some organizations frequently rehire former interns or contractors. In these cases, users may already exist in Azure AD and ImmyBot, allowing immediate device reassignment through this workflow.

However, for brand-new hires:

- The user does not exist in Azure or ImmyBot at submission time
- Device assignment cannot occur until directory synchronization is complete

**Potential Enhancement:**  
Trigger an ImmyBot Azure sync after Microsoft 365 onboarding completes to enable automatic device assignment for newly created users.

---

### Onboarding Customizations

Additional customization options can be enabled for each ImmyBot installer, including:

- Tags
- Auto-onboarding behavior
- Default primary user assignments

To apply these customizations:

1. Navigate to the desired **ImmyBot installer option task**.
2. Open the **JSON request body**.
3. Modify the appropriate fields:
   - `ppkgOptions`
   - `onboardingOptions`

This allows fine-grained control over how each installer behaves per client or onboarding scenario.
