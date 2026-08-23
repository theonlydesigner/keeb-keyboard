# Custom Keyboard Build 

## Project Goals
* **Target Layout:** 60% Compact
* **Design Philosophy:** Minimalist with some Color to make it look like a gaming device
* **Why I'm building this:** Well, I have a knack for building things from scratch and I have been planning to buy a keyboard and this can't be any better.
* **What I have learned:** (To be updated at the end of my build)

---

## Build Journal

### Entry 2: Creating Schematics and PCB
* **Time Spent:** 3.5-4hrs
* **Date:** August 23, 2026

**What I did:*
So I downloaded KiCAD the first thing in the morning and hopped on reading the docs side by side. But again since the documents are so vague I went on YouTube and spent 3 hours learning kiCAD. Then I ended up changing my entire keyboard layout plan. (Please provide detailed guides bcz things got real problematic). But as always in the end everything worked out and I completed the Schematic and got to PCB and spent some time but sheer amount of work I had put into Schematic almost made me pass out so I called it a day. 

**What I got stuck on:*U
Knowing what actually everything does and what to select and why was very confusing. Thanks to a YouTube video which helped out as I was on the verge of giving up. 

**Visual Progress:**
![My Schematics](schematic.png) 
![My half built PCB](pcb.png) 

### Entry 1: Completing the Planning Module
* **Time Spent:** 1 and half hour = 1.5 hours
* **Date:** August 22, 2026

**What I did:**
Since the official planning module didn't provide specific steps, I used industry-standard layout tools such as SwillKb, which I found through Google research. I mapped out my keyboard array on Keyboard Layout Editor. I chose a 60% configuration to maximize desk space. After tweaking the design, I exported the raw layout coordinates and ran them through Swillkb Plate Builder to generate a physical DXF blueprint file. I have successfully committed the raw text data and DXF file to this repository.

**What I got stuck on:**
Understanding stabilizer key spacing (like how big to make the Enter or space keys relative to normal 1u keys) took some trial and error, but reviewing community standard layouts on KLE helped me align everything correctly.

**Visual Progress:**
![My Planned Keyboard Layout](keyboard-layout.png)
