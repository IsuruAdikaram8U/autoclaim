# AutoClaim - Smart Motor Insurance Claim & Geo-Targeted Garage Bidding Marketplace

> A digital platform that brings drivers, insurance companies, and repair garages onto a single system to automate the motor accident claim process. It replaces slow, manual, roadside claim handling with instant digital clearance, competitive blind bidding between nearby garages, and real-time repair tracking.

🚧 **Status:** Ongoing - this is a learning project, actively being built and improved. Features are added phase by phase.

## Table of Contents

1. [Overview](#overview)
2. [The Problem](#the-problem)
3. [The Solution](#the-solution)
4. [How It Works (Full Workflow)](#how-it-works-full-workflow)
5. [User Roles](#user-roles)
6. [Features by Module](#features-by-module)
7. [Tech Stack](#tech-stack)
8. [System Architecture](#system-architecture)
9. [Development Phases](#development-phases)
10. [Getting Started](#getting-started)
11. [Project Status & Roadmap](#project-status--roadmap)
12. [Author](#author)

## Overview

When a vehicle accident happens, the current insurance claim process is slow and frustrating. The driver waits on the road for an assessor, only one garage usually gives a repair price, and there is no easy way to track what is happening with the repair.

AutoClaim solves this by connecting three parties on one platform:

- **The Driver** reports the accident instantly from a mobile app with photos and GPS location.
- **The Insurance Company** reviews and clears the claim remotely, then oversees the garage bidding.
- **Nearby Garages** compete to win the repair job through a fair, blind bidding system.

The result is a faster claim process, fair and competitive repair pricing, and full transparency for everyone involved.

## The Problem

The traditional manual claim process has three major weaknesses:

**Time wasting.** After an accident, the driver has to stop the vehicle and wait on the road, sometimes for hours, until an insurance assessor arrives on-site to inspect the damage. The vehicle cannot be moved until this happens, which blocks traffic and wastes everyone's time.

**Price monopoly and no competition.** Usually only one garage provides a repair quotation. There is no competition, so the insurance company often ends up paying more than a fair market price, and the customer has no real choice.

**Lack of transparency.** Once the vehicle goes to the garage, the driver has no way to know the repair progress. There are no status updates, and the customer is left guessing when the vehicle will be ready.

## The Solution

AutoClaim addresses each of these problems directly:

**Instant digital clearance.** Instead of waiting for an assessor on the road, the driver uploads live GPS location and accident photos through the app. A remote assessor at the insurance company reviews them and approves the claim quickly, giving the driver permission to move the vehicle off the road.

**Blind bidding engine.** The repair request is sent only to verified garages within a set distance (for example, 10 to 15 km) of the accident location. These garages submit competitive estimates. Crucially, no garage can see another garage's bid, which keeps the competition fair and honest.

**Real-time lifecycle tracking.** From the moment the vehicle is handed to the garage until the repair is finished, the customer and insurance company receive live status updates on the repair progress.

## How It Works (Full Workflow)

### Step 1: Incident lodging and severity routing

The driver opens the mobile app at the accident location and submits the incident: GPS location (auto-detected), damage photos, a description of the collision, and one important choice - **Is the vehicle drivable? (Yes / No)**.

The system then routes the claim based on severity:

**Drivable damage (minor or moderate accidents).** The driver submits photos and GPS location. A remote assessor gives instant clearance. The driver can then drive the vehicle away. A fast bidding window (around 15 to 20 minutes) opens for nearby garages.

**Non-drivable or severe damage (vehicle cannot be moved).** The driver selects "Cannot Drive." An automatic towing truck request is triggered, and the driver can track the tow truck live on a map. The vehicle is taken to a temporary holding yard or the driver's home. An extended bidding window (around 2 to 4 hours) opens for garages.

### Step 2: Instant digital clearance

The insurance officer or remote assessor reviews the submitted photos and damage severity from their web portal. Once satisfied, they give instant clearance and a digital reference number is generated. This is what allows the driver to legally move the vehicle off the road without waiting for someone to physically arrive.

### Step 3: Blind bidding by nearby garages

Once cleared, the system automatically sends an anonymous notification to verified garages within the set radius of the accident location. This notification contains only the necessary details: vehicle model, damaged parts, and photos.

Each garage reviews the photos and submits an estimate containing:

- Estimated parts cost
- Estimated labour cost
- Estimated repair duration

Because this is **blind bidding**, no garage can see what any other garage has bid. Each one bids based only on their own honest assessment of the damage.

Note that this first estimate is an **approximate** figure based on photos, which reflects exactly how the real world works. Garages give an initial estimate from photos, and the final exact cost is confirmed later once the vehicle is physically opened up and inspected.

### Step 4: Dual-approval selection (the key logic)

This is a two-stage approval process, designed to be both fair and fraud-resistant.

**Stage 1 - Insurance pre-approval.** All incoming bids first go to the insurance officer. They review the labour and parts costs, remove any bids that are overpriced or unreasonable, and shortlist the best few fair bids (for example, the best 3 out of 5).

**Stage 2 - Customer final choice.** The shortlisted bids are then sent to the customer's mobile app with a notification. The customer browses the approved garages and chooses their preferred one based on three factors: repair duration, garage star rating, and distance from home.

**Why this two-stage design?** If the customer saw all bids directly, they could pick a fake, inflated bid from a friend's garage, which is a form of fraud. By having the insurance company filter first, the insurance company secures a fair cost, and the customer still gets the freedom to choose the garage that best suits them among trustworthy options.

### Step 5: Repair and final estimate

The customer's chosen garage receives the job. The vehicle goes to that garage, where it is physically opened up and inspected properly. If there is hidden damage that was not visible in the photos, the garage can submit an updated estimate (a supplementary estimate). The insurance company reviews and approves this update, and the customer is notified of the change.

The repair then proceeds, and the customer tracks each stage live: Parts Ordered → Body Work → Paint → Ready for Pickup.

## User Roles

| Role | Description | Platform |
|------|-------------|----------|
| **Driver / Customer** | Reports accidents, tracks tow trucks, browses shortlisted quotes, selects a garage, and tracks repair progress. | Mobile App (Flutter) |
| **Insurance Officer / Admin** | Reviews claims, gives digital clearance, vets and shortlists bids, verifies and manages garages. | Web Portal (React) |
| **Garage** | Receives geo-targeted job alerts, submits blind quotations, and updates repair progress. | Web Dashboard (React) |
| **Towing Operator** | Receives automated dispatch alerts for severe accidents and broadcasts live location. | Mobile / Web API |

## Features by Module

### Driver / Customer Mobile App (Flutter)

- **Incident lodgement** with GPS auto-detect, damage photos, collision description, and the "Is Drivable? (Yes/No)" choice.
- **Instant digital clearance** with a digital reference card to allow the vehicle to be moved off the road.
- **Live tow truck tracker** showing the tow truck's route and estimated time of arrival on a map (for non-drivable cases).
- **Shortlisted quotes browser** to compare the insurance-approved bids by price, estimated days, and garage star ratings before choosing a final garage.
- **Live repair stage tracker** to follow the repair step by step, from parts ordered to ready for pickup.

### Insurance Officer / Admin Web Portal (React)

- **Claim assessment panel** showing a real-time queue of submitted claims with high-resolution photos, to check damage severity and give instant clearance.
- **Bidding monitor** to watch the progress of bids sent to nearby garages, along with a countdown timer.
- **Quotation vetting and shortlisting** to review the labour and parts costs of each bid and forward only the fair ones to the customer.
- **Garage verification and blacklisting** to verify documents of registered garages and blacklist any that commit fraud or overcharge.

### Garage Portal (React Web Dashboard)

- **Geo-targeted job alerts** delivered instantly via Socket.io for accidents within the garage's service radius.
- **Blind quotation submission** where the garage reviews the vehicle model and damage photos, then enters parts cost, labour cost, and repair duration.
- **Job progress manager** to update repair stages and upload additional photos as the work proceeds.

### Towing Operator Interface (Flutter / Web API)

- **Automated dispatch alert** with pickup coordinates and holding yard location for severe accidents.
- **Live location broadcast** streaming the tow truck's GPS location to the driver and the insurance dashboard.

## Tech Stack

Everything in this project is built using free or free-tier tools, so the entire system can be developed without cost.

### Backend

- **Node.js + Express.js** for the core REST APIs, authentication, the claim state machine, and role-based access control (RBAC).
- **Socket.io** as the real-time engine for the live bidding timer, instant damage alerts, and status updates.

### Database

- **PostgreSQL** as the primary relational database for users, claims, bids, and transactions.
- **PostGIS** (PostgreSQL extension) as the spatial engine to match garages within a 10 to 15 km radius using geographic queries (`ST_DWithin`).

### Web Frontend

- **React.js + Tailwind CSS** for the insurance officer portal and the garage dashboard.

### Mobile App

- **Flutter (Dart)** for the driver mobile app, handling the camera, maps, and claim tracking.

### Services and Integrations

| Service | Technology | Role |
|---------|-----------|------|
| **Maps & Routing** | Google Maps API | Location picker, garage coordinates, navigation |
| **Payment Gateway** | Stripe (Test Mode) | Policy excess payments (card simulation) |
| **Email OTP** | Nodemailer + Gmail SMTP | 6-digit email verification at registration |
| **SMS OTP** | Firebase Phone Auth / Dev Mock | Phone number verification at registration |
| **Media Storage** | AWS S3 (via AWS SDK v3) | Accident photos, videos, and assessment PDFs via secure presigned URLs |
| **Push Alerts** | Firebase Cloud Messaging (FCM) | Background push alerts to mobile and web |

### About the media storage choice

AWS S3 is used instead of a simpler service for a reason. Files are not uploaded through the backend server directly. Instead, the app asks the backend for a **presigned upload URL**, the backend generates one using the AWS SDK, and the app then uploads the file straight to S3. This keeps heavy photo and video traffic off the backend server, which is the industry-standard way to handle file uploads at scale.

## System Architecture

The platform follows a client-server architecture with a real-time layer:

- **Clients:** A Flutter mobile app (drivers, towing operators) and React web portals (insurance officers, garages) communicate with the backend over REST APIs.
- **Backend:** A Node.js and Express.js server handles business logic, authentication, RBAC, and the claim state machine.
- **Real-time layer:** Socket.io pushes live updates for bidding timers, job alerts, and repair status changes.
- **Database:** PostgreSQL stores all relational data, and PostGIS handles location-based garage matching.
- **External services:** AWS S3 for media, Google Maps for location and routing, Stripe for payments, and Firebase for push notifications and SMS OTP.

The core of the backend is a **claim state machine** that moves each claim through clearly defined stages, from lodged, to cleared, to bidding, to shortlisted, to assigned, to in-repair, to completed.

## Development Phases

This project is being built in phases. Rather than building everything at once, the goal is to first complete a working core system (MVP), then add advanced features on top of it.

### Phase 1 - MVP (Core Flow)

The essential end-to-end flow that makes the system work:

- Driver reports an incident with photos and GPS location.
- Insurance officer reviews and gives digital clearance.
- Blind bid request is sent to nearby garages (using PostGIS radius matching).
- Garages submit blind estimates.
- Insurance officer shortlists the fair bids.
- Customer selects a garage from the shortlist.
- Basic repair status tracking.

### Phase 2 - Severity Routing & Towing

- The "Is Drivable?" decision and severity-based routing.
- Automatic towing dispatch for severe accidents.
- Live tow truck tracking.
- Holding yard and extended bidding window logic.

### Phase 3 - Estimates, Payments & Trust

- Supplementary estimates (updating the cost after physical inspection) with insurance approval.
- Stripe payment integration for policy excess.
- Garage ratings and reviews.
- Garage verification and blacklisting.

### Phase 4 - Polish & Advanced

- Full push notification system.
- Assessment PDF generation and storage.
- Analytics dashboards for the insurance company.
- Refinements based on testing.

## Getting Started

> Setup instructions will be added as the project develops. The repository will be organized into separate folders for the backend, web frontend, and mobile app.

A typical structure will look like this:

```
autoclaim/
├── backend/        # Node.js + Express.js API
├── web/            # React web portals (insurance + garage)
└── mobile/         # Flutter driver app
```

## Project Status & Roadmap

This is an ongoing learning project. It is being built step by step as a way to learn a new technology stack (Node.js, Express, Socket.io, PostgreSQL with PostGIS, React, Flutter, and AWS S3) while solving a real-world problem.

Current focus is on Phase 1, the core claim and bidding flow. Progress will be updated here as the project grows.

## Author

Built as a self-learning project to explore full-stack development, real-time systems, geospatial queries, and cloud storage while solving a practical problem in the motor insurance industry.
