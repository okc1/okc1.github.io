---
layout: post
title: "[CC150v5] 12.0 Example - Troubleshoot Google Chrome "
comments: true
categories:
- CC150v5
- z-testing

---

### Question

> You'reworking on the Google Chrome team when you receivea bug report: Chrome crashes on launch. What would you do? 

### Step 1: Understand the Scenario

1. How long has user seen this issue?
1. version of browser and OS?
1. Does this happen consistently? How often, and when?

### Step 2: Break Down the Problem

Flow of situation:

1. start menu
1. click chrome
1. browser starts
1. browser load settings
1. browser issues HTTP response
1. browser get HTTP response
1. browser parses webpage
1. browser displays content

__At some points in this process, something fails__. A good tester would iterate thru the elements of this scenario and diagnose the problem. 

### Step 3: Create Specific, Manageable Tests

Come up with realistic instructions. 
