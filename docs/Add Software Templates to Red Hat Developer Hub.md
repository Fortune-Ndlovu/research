# Adding Software Templates to Red Hat Developer Hub

This guide outlines the steps required to add software templates to the Red Hat Developer Hub. Software templates provide standardized scaffolding for creating new software components or services, ensuring consistency and speeding up development processes.

---

## Prerequisites

1. Red Hat Developer Hub (RHDH) Access:
    - Ensure you have access to an RHDH instance with the required permissions.
2. Backstage Knowledge:
    - Familiarity with Backstage's Software Templates functionality.
3. Template Configuration File:
    - A `template.yaml` file that defines the template specification.

---

## Step-by-Step Guide

### 1. Prepare Your Template Repository

1. Create a Repository:
    - Set up a Git repository for your template.
    - Use a clear naming convention (e.g., `template-[template-name]`).
2. Add Template Files:
    - Include all necessary files for your software project.
    - Ensure the `template.yaml` file is located in the root directory.
3. Validate the `template.yaml`:
    - The `template.yaml` file must follow the Backstage Template Schema.
    - Example:

    ```yaml
    apiVersion: scaffolder.backstage.io/v1beta3
    kind: Template
    metadata:
      name: my-template
      title: My Software Template
      description: A template to create a new service.
    spec:
      owner: team@example.com
      type: service
      parameters:
        - title: Service Name
          type: string
          required: true
      steps:
        - id: fetch
          name: Fetch from repository
          action: fetch:plain
          input:
            url: '{{ parameters.repositoryUrl }}'
    ```

---

### 2. Host the Template Repository

1. Push the Repository:
    - Push the template repository to a Git hosting platform (e.g., GitHub, GitLab, Bitbucket, or an internal Git server).
2. Provide Access:
    - Ensure the Red Hat Developer Hub instance has access to the repository.

---

### 3. Add the Template to RHDH

1. Access RHDH:
    - Log in to your RHDH instance.
2. Navigate to the Backstage Catalog:
    - Go to `Catalog` > `Create`.
3. Register the Template:
    - Click on `Register Existing Component`.
    - Enter the URL of the `template.yaml` file.
    - Validate and confirm the registration.
4. Categorize the Template:
    - Assign appropriate categories and tags for easy discovery.

---

### 4. Verify Template Functionality

1. Test the Template:
    - Navigate to `Create` > `Available Templates`.
    - Select your template and fill in the required parameters.
    - Validate the scaffolding process by completing the form.
2. Fix Issues (if any):
    - Debug and fix errors in the `template.yaml` or associated files.

---

### 5. Publish Template for Team Use

1. Update Documentation:
    - Document the template usage for your team.
    - Include parameter descriptions and example use cases.
2. Announce Availability:
    - Inform your team about the new template via email, chat, or a team meeting.

---

## Best Practices

- Template Updates:
    - Use semantic versioning for template updates.
    - Communicate breaking changes clearly.
- Parameter Validation:
    - Include validation rules to ensure proper input values.
- Template Discovery:
    - Use clear titles, descriptions, and tags to improve discoverability.
