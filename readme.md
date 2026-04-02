# Original App Design Project

## StudyBuddy

## Table of Contents
1. [Overview](#overview)
2. [Product Spec](#product-spec)
3. [Wireframes](#wireframes)
4. [Schema](#schema)

## Overview

### Description
StudyBuddy is a gamified mobile app that helps college students find and create study groups for their courses. Users post study sessions, check in when they arrive to earn XP, build daily study streaks, and compete on course-specific leaderboards. The app turns studying from a chore into a rewarding, social habit.

### App Evaluation

- **Category:** Education / Social / Gamification
- **Mobile:** Location-based check-ins (GPS verification at study spots), push notifications for streak reminders and leaderboard changes, real-time chat. The mobile experience is essential — students check in and track progress on the go.
- **Story:** Studying alone is less effective and harder to stay motivated. StudyBuddy adds game mechanics — XP, streaks, leaderboards, and badges — so students are rewarded for showing up consistently. It connects students who share courses and turns study habits into friendly competition.
- **Market:** College and university students. Gamification appeals strongly to achievement-driven and competitive students. Could expand to high school or professional certification prep.
- **Habit:** Very high frequency — the streak system and daily XP rewards incentivize daily engagement. Leaderboard competition keeps users coming back even outside of exam season. Users both create and consume sessions.
- **Scope:** V1 focuses on sessions, check-ins, XP, and a basic leaderboard. V2 adds streaks, badges, and real-time chat. V3 could add reward tiers, course integration, and calendar sync. The core MVP is achievable within the project timeline.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

- [x] User can register a new account
- [x] User can log in and log out
- [x] User can create a study session (course, topic, location, date/time, max group size)
- [x] User can browse a feed of upcoming study sessions
- [x] User can join an existing study session
- [x] User can check in to a session (location-verified) and earn XP
- [x] User can view their XP total, current streak, and level on their profile
- [x] User can view a leaderboard ranked by XP (weekly and all-time)
- [x] User can view details of a study session including members

**Optional Nice-to-have Stories**

- [ ] User can earn badges for milestones (e.g., "First Session", "7-Day Streak", "Top 3 Finish")
- [ ] User can view a course-specific leaderboard (e.g., top studiers in CS 101)
- [ ] User can receive streak reminder push notifications ("Don't lose your 5-day streak!")
- [ ] User can search/filter sessions by course or subject
- [ ] User can chat with study group members in real-time
- [ ] User can view study sessions on a map
- [ ] User can unlock reward tiers (Bronze, Silver, Gold) based on cumulative XP
- [ ] User can persist login across app restarts

### 2. Screen Archetypes

- **Login Screen**
  - User can log in
- **Registration Screen**
  - User can register a new account
- **Session Feed Screen**
  - User can browse upcoming study sessions
  - User can pull to refresh the feed
- **Session Detail Screen**
  - User can view session details (course, topic, location, time, members)
  - User can join a study session
  - User can check in to the session (GPS-verified) and earn XP
- **Create Session Screen**
  - User can create a new study session with all required fields
- **Leaderboard Screen**
  - User can view weekly and all-time XP rankings
  - User can toggle between global and course-specific leaderboards
- **Profile Screen**
  - User can view their XP, level, current streak, and badges
  - User can view their created and joined sessions
  - User can log out

### 3. Navigation

**Tab Navigation (Tab to Screen)**

- Home Feed
- Create Session
- Leaderboard
- Profile

**Flow Navigation (Screen to Screen)**

- **Login Screen**
  - Leads to **Registration Screen** (tap "Sign Up")
  - Leads to **Session Feed Screen** (upon successful login)
- **Registration Screen**
  - Leads to **Session Feed Screen** (upon successful registration)
- **Session Feed Screen**
  - Leads to **Session Detail Screen** (tap on a session card)
- **Session Detail Screen**
  - Leads back to **Session Feed Screen** (back button)
- **Create Session Screen**
  - Leads to **Session Feed Screen** (after session is created)
- **Leaderboard Screen**
  - Leads to **Profile Screen** (tap on a user)
- **Profile Screen**
  - Leads to **Session Detail Screen** (tap on a session)
  - Leads to **Login Screen** (log out)

## Wireframes

### [BONUS] Digital Wireframes & Mockups

#### Login, Registration & Session Feed Screens
<img src="wireframes/wireframes_page1.png" width="600"/>

**Login Screen** — App logo centered at top, Email and Password input fields, **LOG IN** primary action button, **SIGN UP** secondary button navigates to Registration.

**Registration Screen** — Input fields: Username, Email, Password, Confirm Password, University, Major (optional). **CREATE ACCOUNT** primary action button.

**Session Feed Screen** — "Study Sessions" header with scrollable list of session cards. Each card shows a course badge (CS 101, MATH 250, ENG 102, PHYS 201), topic preview, member count with group icon (e.g., 3/5), and a "FULL" indicator when at capacity. Bottom tab bar: **Feed** | Create | Board | Profile.

#### Session Detail, Create Session & Leaderboard Screens
<img src="wireframes/wireframes_page2.png" width="600"/>

**Session Detail Screen** — Course badge at top (e.g., CS 101), session info card with Date, Time, Location, and Members count, member avatar circles, **JOIN SESSION** primary action button, **CHECK IN (50 XP)** secondary button for GPS-verified attendance.

**Create Session Screen** — Form fields: Course, Study topic, Location, Date, Time, Max members. Bottom tab bar with **Create** tab highlighted.

**Leaderboard Screen** — **Weekly** / **All-Time** toggle at top.
- Top 3 podium display with rank badges (#1, #2, #3) and XP totals (680, 450, 320 XP)
- Ranked list below podium showing #4-#6 with avatar, name bar, and XP
- Bottom tab bar with **Board** tab highlighted

#### Profile Screen
<img src="wireframes/wireframes_page3.png" width="300"/>

- Profile avatar and username
- Stats card showing **1,450 XP** | **Level 8** | **5 Streak** (fire icon)
- XP progress bar toward next level
- Badges section with earned badge tiles (4 slots shown)
- Recent sessions list
- Bottom tab bar with **Profile** tab highlighted

### [BONUS] Interactive Prototype

## Schema

### Models

**User**

| Property  | Type   | Description                              |
|-----------|--------|------------------------------------------|
| userId    | String   | unique id for the user (default field)   |
| username  | String   | display name for the user                |
| email     | String   | user's email for login                   |
| password  | String   | user's password for login authentication |
| xp        | Number   | total experience points earned           |
| level     | Number   | current level based on XP thresholds     |
| streak    | Number   | current consecutive days with a check-in |
| longestStreak | Number | all-time longest streak                |
| badges    | Array of Strings | list of earned badge IDs            |
| createdAt | DateTime | date when user account was created       |

**StudySession**

| Property    | Type     | Description                                |
|-------------|----------|--------------------------------------------|
| sessionId   | String   | unique id for the session (default field)  |
| author      | Pointer to User | user who created the session         |
| course      | String   | course name/number (e.g., "CS 101")        |
| topic       | String   | study topic for the session                |
| location    | String   | where the session will be held             |
| dateTime    | DateTime | scheduled date and time of the session     |
| maxSize     | Number   | maximum number of members allowed          |
| members     | Array of Pointers to User | users who joined the session |
| createdAt   | DateTime | date when session was created              |

**CheckIn**

| Property    | Type            | Description                                  |
|-------------|-----------------|----------------------------------------------|
| checkInId   | String          | unique id for the check-in (default field)   |
| user        | Pointer to User | user who checked in                          |
| session     | Pointer to StudySession | the session checked into             |
| xpEarned    | Number          | XP awarded for this check-in                 |
| bonusReason | String          | reason for bonus XP (e.g., "streak_bonus", "group_bonus") |
| createdAt   | DateTime        | timestamp of the check-in                    |

**Badge**

| Property    | Type   | Description                                    |
|-------------|--------|------------------------------------------------|
| badgeId     | String | unique id for the badge                        |
| name        | String | display name (e.g., "7-Day Streak")            |
| description | String | how to earn the badge                          |
| icon        | String | icon/image URL for the badge                   |
| xpThreshold | Number | XP requirement to unlock (if applicable)       |

### XP Reward Rules

| Action                  | XP Earned |
|-------------------------|-----------|
| Check in to a session   | +50 XP    |
| Create a session        | +30 XP    |
| Streak bonus (3+ days)  | +20 XP    |
| Streak bonus (7+ days)  | +50 XP    |
| Group size bonus (5+)   | +15 XP    |
| First session of the week | +25 XP  |

### Networking

**Session Feed Screen**
- `[GET] /sessions` - retrieve all upcoming study sessions

**Session Detail Screen**
- `[GET] /sessions/:id` - retrieve details for a single session
- `[POST] /sessions/:id/join` - join a study session
- `[POST] /sessions/:id/checkin` - check in to a session (awards XP, updates streak)

**Create Session Screen**
- `[POST] /sessions` - create a new study session

**Leaderboard Screen**
- `[GET] /leaderboard?period=weekly` - retrieve weekly XP rankings
- `[GET] /leaderboard?period=alltime` - retrieve all-time XP rankings
- `[GET] /leaderboard?course=CS101` - retrieve course-specific rankings

**Profile Screen**
- `[GET] /users/:id` - retrieve user profile data (XP, level, streak, badges)
- `[GET] /users/:id/sessions` - retrieve sessions created/joined by user
- `[GET] /users/:id/checkins` - retrieve user's check-in history

**Login / Registration**
- `[POST] /users/login` - authenticate user
- `[POST] /users/register` - create a new user account
