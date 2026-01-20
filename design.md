# Technical Design Document: Zero Delta LLC Landing Page

**Author:** Dave Schmidt
**Date:** January 2026
**Version:** 1.0

## 1. Executive Summary

The goal is to deploy a low-maintenance, high-performance "digital business card" for Zero Delta LLC. The site serves as a quick reference point for potential clients and contracting partners. It prioritizes security, minimalism, and speed over marketing flair.

## 2. Infrastructure Architecture

### Primary Domain: `zerodelta.dev`

- **Hosting:** AWS S3 (Static Website Hosting enabled).
- **Distribution:** AWS CloudFront (HTTPS termination, HTTP/2).
- **DNS:** AWS Route53 (Alias record pointing to CloudFront).
- **Security:** ACM Certificate (TLS 1.2+).

### Secondary Domain: `zdelta.dev`

- **Function:** Pure 301 Redirect to `zerodelta.dev`.
- **Implementation:** S3 redirect bucket -> `https://zerodelta.dev`; CloudFront uses the **S3 Website Endpoint**; Viewer Protocol Policy set to "Redirect HTTP to HTTPS".

## 3. Frontend Specifications

### Core Philosophy

- **No Frameworks:** Raw HTML5 and CSS3 only. No React, Vue, or Bootstrap.
- **Single File:** CSS embedded in `<head>` to minimize HTTP requests.
- **Privacy:** Zero cookies, zero tracking pixels, zero external scripts.

### Visual Identity ("The Terminal Standard")

- **Theme:** Dark Mode Native.
- **Color Palette:** Background `#0d1117`; Text `#c9d1d9`; Accent `#58a6ff`; Status Green `#2ea043`.
- **Typography:** Monospace Stack (`'Courier New', Courier, monospace`).
- **Layout:** Vertical column, centered max-width (600px), mobile-responsive padding.

## 4. Content Strategy

### Header

- **Logo:** Text-based `> ZERO DELTA LLC` with a CSS blinking cursor animation (`_`).
- **Tagline:** "Cloud Architecture & Infrastructure Automation."

### Status Block

- **Indicator:** CSS-generated green circle.
- **Text:** "Status: OPERATIONAL".

### Contact & Profiles

- **Contact:** Mailto link (`dave@zdelta.dev`).
- **Social Proof:** Links to GitHub (Code) and LinkedIn (Resume).

### Footer

- **Legal:** "Registered: Commonwealth of Virginia".
- **Compliance:** "C2C Ready | W-9 Available on Request".

## 5. Deployment Strategy

- **Version Control:** Local Git repository.
- **Deployment:** AWS CLI sync command: `aws s3 sync . s3://zerodelta-web-root --delete` then `aws cloudfront create-invalidation --distribution-id DIST_ID --paths "/*"`.
