---
name: classroom-manager
description: List existing Google Classroom courses or create a new one using the Google Classroom API.
metadata:
  require-secret: true
  require-secret-description: "Please enter your Google OAuth token (requires the classroom.courses scope). You can obtain one from the Google OAuth 2.0 Playground at https://developers.google.com/oauthplayground"
---

# Classroom Manager

## Instructions

Call the `run_js` tool with a JSON string for `data` containing the following fields:

- **action**: Required. Either `"list"` or `"create"`.
  - `"list"`: Returns all courses visible to the authenticated user.
  - `"create"`: Creates a new course.

- **courseName**: Required when action is `"create"`. The name of the course (1–750 characters).

- **ownerId**: Optional. Used with `"create"`. The owner of the course (email, numeric ID, or `"me"`). Defaults to `"me"`.

- **section**: Optional. Used with `"create"`. The section label (e.g., "Period 2").

- **description**: Optional. Used with `"create"`. A description of the course.

- **room**: Optional. Used with `"create"`. The room location (e.g., "301").

### Examples

To list courses, call `run_js` with:
```json
{"action": "list"}
```

To create a course, call `run_js` with:
```json
{"action": "create", "courseName": "10th Grade Biology", "section": "Period 2", "room": "Lab 3"}
```

### Interpreting Results

- On **list**: The result contains a `courses` array. Present each course's `name`, `courseState`, and `alternateLink` to the user. If the array is empty, tell the user they have no courses.
- On **create**: The result contains the newly created course object. Confirm creation by showing its `name`, `id`, `enrollmentCode`, and `alternateLink`.
- On **error**: The result contains an `error` string. Relay the error message to the user.
