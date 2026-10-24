# NivasConcierge (Kadamba Concierge)

## Overview

NivasConcierge is a QR-enabled hotel guest-service and staff-coordination system designed to help hotels manage guest requests across departments from one shared interface.

Guests scan a QR code in their room to open the guest request page. Hotel staff can view incoming requests, accept them, track their progress, and mark them as completed.

**Core value proposition:** Every guest request captured. Every task tracked. Every department connected.

Demo: https://nivasconcierge.netlify.app/

## Problem Statement

Independent hotels and resorts often manage guest requests through phone calls, verbal instructions, paper notes, and fragmented messaging. These workflows can lead to missed requests, delayed service, unclear task ownership, repeated follow-ups, and limited visibility for hotel management.

NivasConcierge aims to centralise guest requests and make their status visible to the teams responsible for completing them.

## Key Features

- **QR-based guest access:** Guests scan a room QR code to open the request page.
- **No guest sign-in:** Guests can submit requests without creating an account.
- **Shared staff interface:** Staff can see requests and their current status.
- **Request lifecycle:** Staff can accept a request and mark it as completed.
- **Department coordination:** Supports workflows involving areas such as Reception, Housekeeping, Kitchen, and Maintenance.
- **Live request visibility:** Staff can see new, in-progress, and completed requests in the interface.
- **Voice and text commands:** The demonstrated staff interface includes a voice/microphone control and a text command field at Reception.
- **Multilingual interface:** The demonstrated interface lists English, Hindi, Kannada, Tamil, and Telugu.

> Feature availability and behaviour should be confirmed against the current deployed version before making customer-facing promises.

## How It Works

1. A guest scans the QR code associated with their room.
2. The guest selects a service or submits a request.
3. The request appears in the staff interface.
4. The responsible staff member accepts the request.
5. Staff complete the task and update its status.
6. The guest can see the request's progress.

## Intended Users

- Hotel guests
- Reception and front-desk staff
- Housekeeping teams
- Kitchen and room-service teams
- Maintenance staff
- Hotel owners and managers

## Expected Benefits

NivasConcierge is designed to help hotels:

- Reduce the chance of requests being overlooked.
- Make request ownership and progress easier to see.
- Improve coordination between departments.
- Reduce repeated follow-ups about request status.
- Give managers better visibility into day-to-day guest-service operations.
- Provide guests with a simple digital way to request assistance.

These are intended benefits, not guaranteed results. Hotels should measure outcomes during a pilot.

## Suggested Pilot Metrics

To evaluate the system at a hotel, track:

- Number of requests received
- Time from request submission to staff acknowledgement
- Time from submission to completion
- Number and percentage of requests still open
- Requests by department and category
- Guest feedback and staff feedback

Compare results with the hotel's existing process before claiming specific improvements.

## Demo Walkthrough

Use the demo to explore the guest and staff experiences:

1. Open the demo website.
2. Explore the guest-phone view and submit a sample request if available.
3. Open the reception/staff view.
4. Observe how requests appear and how their status can be updated.
5. Explore the room and department workflows available in the current demo.

Demo URL: https://nivasconcierge.netlify.app/

## Positioning

Position NivasConcierge as a **hotel guest-request and staff-coordination system**, rather than only a QR concierge page. Its central workflow is to capture a request, make it visible to the responsible team, and track it through completion.

## Current Scope and Limitations

This README describes the product based on the available demo and product information. It does not document the source-code architecture, installation commands, environment variables, database, APIs, authentication implementation, or deployment pipeline because those technical details have not been provided here.

Before production use, confirm operational requirements such as connectivity, staff permissions, guest privacy, request retention, escalation rules, integrations, and support arrangements.

## Contact

For product demonstrations or business enquiries, use the contact details provided by the NivasConcierge / NO-FOMO team.

---

*README prepared from the available NivasConcierge demo and product description. Update this file as implementation details and features are confirmed.*
