# BluePrint 🔵

A unified course planning and academic advising platform for Duke University students.

## Overview

DukeHub tells you what courses exist. The undergraduate bulletin tells you what you need. RateMyProfessor tells you who to take. Your advisor tells you if it all fits together.

BluePrint brings all of that into one place.

Built on real Duke course data pulled directly from Duke's Streamer OIT API, BluePrint helps students search courses, plan their schedule around real Fall section times, compare options with AI, and get personalized academic guidance — all without leaving a single tab.

## Features

**Course Search**
Filter Duke's full catalog of 9,940 courses by subject, level, keyword, and curriculum requirements. Supports both the classic Duke curriculum (Areas of Knowledge and Modes of Inquiry) and the new 2025 Arts & Sciences curriculum (CE, HI, IJ, NW, QC, SB distribution categories).

**Smart Scheduler**
Add the courses you're registered for by selecting specific sections — with real Fall 2026 meeting times sourced from Duke's API. Set preferences like earliest start time, days to avoid, and requirements to fulfill. BluePrint finds conflict-free courses that fit around your existing schedule.

**Compare Courses**
Select any two Duke courses and get an AI-powered breakdown of similarities, differences, Areas of Knowledge and Modes of Inquiry alignment, and career preparation — powered by GPT-4.1 Nano.

**Programs Directory**
Browse all 141 Duke undergraduate programs — 70 bachelor's degrees, 51 minors, and 20 certificates — with direct links to official requirement pages in the undergraduate bulletin.

**Course Optimizer**
Select multiple degree requirements simultaneously and find courses that satisfy all of them at once. Designed for students strategically planning how to fulfill remaining requirements with minimal course load.

**Professor Ratings**
Search any Duke professor and instantly see their RateMyProfessor overall rating, difficulty score, and percentage of students who would take them again.

**Bluebot**
An AI academic advisor with deep knowledge of Duke's curriculum — both the pre-2025 and 2025+ Trinity requirements, and both Pratt School of Engineering curriculum versions. Ask anything about courses, requirements, or degree planning.

**Profile & Authentication**
Create an account with your Duke NetID. A 6-digit verification code is sent to your `netid@duke.edu` address — ensuring only verified Duke students can register. Track completed courses and build your academic profile.

## Tech Stack

- **Backend:** Python, Flask, PostgreSQL
- **Frontend:** React, Vite, React Router
- **AI Proxy:** Node.js, Express
- **AI Model:** GPT-4.1 Nano via Duke's LiteLLM proxy
- **Authentication:** bcrypt, SendGrid email verification
- **Data:** Duke Streamer OIT API, RateMyProfessor GraphQL API

## Database

PostgreSQL database seeded from Duke's official Curriculum API:

- 9,940 courses across all departments
- 5,420 Fall 2026 course sections with days, times, and locations
- Classic curriculum codes (AOK/MOI) and new 2025+ distribution codes
- 141 undergraduate programs (majors, minors, certificates)

## Getting Started

**Prerequisites**
- Python 3.13+
- Node.js 18+
- PostgreSQL
- Duke Streamer API key
- Duke LiteLLM API key
- SendGrid API key with a verified sender

**Environment Variables**

Create a `.env` file with:
DUKE_API_KEY=your_duke_api_key
SENDGRID_API_KEY=your_sendgrid_key
SENDGRID_FROM_EMAIL=your_verified_email
OPENAI_API_KEY=your_duke_litellm_key
BASE_URL=https://litellm.oit.duke.edu

**Setup**
```bash
# Create and seed the database
createdb duke_courses
python3 seed.py
python3 seed_attributes.py
python3 seed_new_aok.py
python3 seed_programs.py
python3 seed_offerings.py  # pulls Fall 2026 data from Duke API (~20 mins)

# Start the backend
python3 app.py  # runs on :5001

# Start the AI proxy
node backend/server.js  # runs on :3001

# Start the frontend
cd essentialfiles
npm install
npm run dev  # runs on :5173
```

## Roadmap

- Study abroad course integration (GEO database)
- Degree audit tracking against program requirements
- Instructor names for Fall sections (not yet available at Duke Streamer OIT API)
- Duke SSO authentication for production deployment
- RateMyProfessor ratings within the Smart Scheduler once instructor data is available