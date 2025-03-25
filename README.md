# Salesforce-based task management system

A Salesforce-based task management system that provides REST API endpoints for task operations and includes Lightning Web Components for task visualization.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Testing](#testing)
- [Limitations](#limitations)
- [Security Considerations](#security-considerations)

## Overview

This project implements a custom task management solution in Salesforce, featuring:

- ✅ Custom Task Object for task management.
- ✅ REST API endpoints for task operations.
- ✅ Lightning Web Components (LWC) for task visualization.
- ✅ Batch/Queueable Apex jobs for automated task processing.
- ✅ OAuth-secured API authentication.

## Features

- ✔ REST API for Task Management – Fetch, create, update, and delete tasks via API.
- ✔ Lightning Web Component UI – Interactive interface for managing tasks.
- ✔ Batch Processing – Automates large-scale task updates.
- ✔ OAuth Authentication – Secure access to API endpoints.
- ✔ Governor Limit Compliance – Optimized to handle Salesforce limits.

## Installation

### Prerequisites

- Salesforce CLI installed
- Dev Hub org enabled
- Visual Studio Code with Salesforce extensions

### Deployment Steps

1. Clone this repository:

   ```bash
   git clone https://github.com/MuindiStephen/Salesforce-based-taskmanager-technicalAssessment-BidhaaSasa.git
   cd salesforcebasedtaskmanager-bidhaaSasa
   ```

2. Authorize your Salesforce org

   ```bash
   sfdx auth:web:login -d -a TaskManagerOrg
   ```

3. Deploy the source:

   ```bash
   sfdx force:source:deploy -p force-app/main/default
   ```

4. Assign required permissions 

   ```bash
   sfdx force:user:permset:assign -n TaskManagerPermissionSet
   ``` 

## Configuration

### Setting Up the Lightning Web Component (LWC)

1. Open Setup in Salesforce.
2. Navigate to Lightning App Builder.
3. Create a new Lightning Page.
4. Drag the `taskManager` component onto the page.
5. Activate and assign the page to user profiles

### Configuring API Access

1. Create a Connected App in Setup.
2. Activate and assign the page to user profiles
  - Add callback URL:
   ```bash
    https://orgfarm-09d8fb4aca-dev-ed.develop.my.salesforce.com/
   ``` 
  - Select OAuth Scopes:
    - ✅ Access API (api)
    - ✅ Perform requests (refresh_token, offline_access)
3. Save & note down Consumer Key & Secret

## Usage

### REST API Endpoints

Base URL: 

#### Available Endpoints:

```http
GET    https://orgfarm-09d8fb4aca-dev-ed.develop.my.salesforce.com/services/apexrest/Tasks
         # Retrieve all tasks
```

### Sample API Calls

#### Fetch Tasks (using cURL):

```bash
curl -X GET \  
  'https://orgfarm-09d8fb4aca-dev-ed.develop.my.salesforce.com/services/apexrest/Tasks'
```

### Running Batch Jobs

1. Open Developer Console.
2. Execute Anonymous Apex:

   ```apex
   TaskProcessingBatch batch = new TaskProcessingBatch();
   Database.executeBatch(batch);
   ```

## Testing

### Apex Tests

Run all tests using:

```bash
sfdx force:apex:test:run -l RunLocalTests -r human
```

### LWC Testing

1. Run Jest tests:

   ```bash
   npm run test:unit
   ```

2. Manual Testing:

    - Access the Lightning page containing the component.
    - Verify CRUD operations.
    - Test error scenarios.

## Limitations

- ⚠ Governor Limits – API calls and batch operations are subject to Salesforce limits.
- ⚠ Bulk Operations – Limited to 10,000 records per operation.
- ⚠ Session Timeout – OAuth tokens expire after 2 hours of inactivity.

## Security Considerations

- 🔒 Enforced Field-Level Security (FLS)
- 🔒 CRUD Permissions Verified
- 🔒 Rate Limiting Applied to API Calls
- 🔒 OAuth-based Authentication for API Access
