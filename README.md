# AutoMAYtion2026: Immybot Onboarding Handler
This automation adds additional features to the functionality of Rewst's Microsoft: User Onboarding Crate. By providing some additional options on the Onboarding form, this autoamtion can automatically generate your choice of ImmyBot Installer and add it to the onboarding ticket. If the user is to recieve a machine already deployed on site, you can instead reassign and begin a maitenance session on that machine so the user is ready to start on day 1!

1. Installation

   This automation assumes you have an Immybot Integation setup in your Rewst environment, and that you have unpacked the Microsoft: User Onboarding Crate. My version uses Connectwise PSA as the ticketing system, but with some tweaks this workflow can be applied to other ticketing solutions.

   Import Form Bundle
   - Navigate to the Immy Onboarding Handler folder and download the form bundle named: form-019cd2be-c5cc-7733-bf99-83356061dfbc_20260312_145611.bundle.json
   - Navigate to the Forms section of Rewst and find the 'Import Bundle' button.
   - Drag and drop the form bundle you downloaded earlier.
   - Review the list of objects to be imported and confirm the selection.
  
   Import Workflow Bundle
   - Navigate to the Immy Onboarding Handler folder and download the worflow bundle named: workflow-019afff1-45af-7079-85c8-9d09a62a4018_20260312_150235.bundle.json
   - Navigate to the Workflows section of Rewst and find the 'Import Bundle' button.
   - Drag and drop the workflow bundle you downloaded earlier.
   - Review the list of objects to be imported and confirm the selection.
  
   Setup Form Trigger
   - Open your Microsoft: User Onboarding workflow in workflow builder and create a new Form Trigger.
   - Assign overrides for Connectwise PSA and Immybot using their organization mappings.
   - Select the new form you just imported.
  
   Setup Completion Handler
   - While stil in your Microsoft: User Onboarding workflow builder, create a new Completion Handler.
   - Select the newly imported workflow, and configure the Immy Onboarding Handler to run on Onboarding success.

2. Usage

   To use this workflow, simply open the new onboarding form for the desired client. After filling in the normal onboarding information, select 'Customize Advanced Options' -> 'Advanced - Immybot Options'
   - To prep an existing computer, select 'Use Existing Computer' and select the Immybot computer and person from the dropdowns.
     - This will cause the selected user to be assigned to the machine in ImmyBot, start a maintenance session for the computer, and update the ticket notes with the session page for the computer.
   - To prep a new computer for this user, select 'New Immy Installer', and then select the radio button of your desired Immybot Installer format.
     - For OOBE, choose the .ppkg option. This will update the ticket notes with a download link for a provisioning package specific to this client.
     - For computers past OOBE, select either the .exe option or the .ps1 option. The .exe option will update the ticket notes with a download link specific to the client. The .ps1 option will attach a Powershell Script file to the ticket attachments.

  By utilizing this completion handler, technicians can onboard new users and start prepping hardware from the same submission form.

3. Improvement Ideas
   Immybot Azure sync after M365 onboard:
   - We have clients that frequently re-hire college interns after they graduate. As a result, these users are often in AD and Immybot from their time as an intern, allowing easy computer reassignment via this workflow. However, for brand new hires it will not be possible to assign them to an immy computer until after they are added to Azure and synced.
   Onboarding Customizations:
   - If desired, additional options can be enabled for each of the ImmyBot installers, such as tags, auto-onboarding, or default primary users. To make these changes, simply navigate to the ImmyBot installer option task of your choice, open the JSON request body and edit the 'ppkgOptions' or 'onboardingOptions' fields with your desired information.
