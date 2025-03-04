# CyberAnalyst-AI-Shadow

Yo, I’m Raj—Master’s in Info Systems and Security, cybersecurity analyst at heart. This project’s my own invention: an AI that shadows me, learning my analyst moves—like how I spot threats in logs—and takes over grunt work. Ain’t no tool like this out there!

What’s the Big Idea?
Analysts like me dig through logs, alerts—tons of noise. My AI watches me work, learns my “threat or nah” calls, and starts doing it for me. It’s like training a mini-me for the boring stuff.

How I Made It Happen

Here’s how I cooked it up:

Log My Moves: Tracked my decisions—like “this Splunk alert’s a port scan, ignore that ping.” Example: “10 hits on port 445—SMB attack!”
Feed the AI: Gave it my calls—alert type, count, my verdict. Example: “Port 445, 10 hits, threat” vs. “Port 80, 5 hits, safe.”
Train It: AI learned my vibe—like “Raj flags 10+ hits as bad.” Macro Detail: Used “XGBoost”—it’s fast and loves decisions. Example: After 20 calls, it guessed like me.
Shadow Me: New alert comes—AI says, “Raj’d call this a threat!” Example: “15 hits on 22—Alert!”
Stuff You’ll Need


Python: python.org—my base.

Helpers:
pandas—log organizer.
xgboost—AI decision maker. Splunk/Wireshark: For logs (or fake ‘em).


Let’s Build It—Step by Step with Commands

Install Python: python.org, 3.11, 
“Add to PATH” checked. 

Command: “python --version”—check for “3.11.x”.

Get Helpers: Command line,
type these and hit enter:
“pip install pandas” (log pal).
“pip install xgboost” (AI champ).

Set Up Folder: You’re in RajCyberAIProjects/CyberAnalystAIShadow—perfect!
Command: “cd RajCyberAIProjects\CyberAnalystAIShadow” (Windows) 
or
“cd RajCyberAIProjects/CyberAnalystAIShadow” (Mac) from main.

Fake Logs: It’s saved as “logs.csv” here—check it:


text

port,hits,verdict
445,10,1
80,5,0
22,15,1
(1 = threat, 0 = safe—you can add more!)

Code It: Saved as “ai_shadow.py” in this folder—take a look:



python

# My analyst twin
import pandas as pd
import xgboost as xgb

# Load my calls
logs = pd.read_csv("logs.csv")

# Train AI
model = xgb.XGBClassifier()
model.fit(logs[["port", "hits"]], logs["verdict"])

# New alert
new_alert = pd.DataFrame([[23, 12]], columns=["port", "hits"])
pred = model.predict(new_alert)
if pred[0] == 1:
    print(f"Alert! Port {new_alert['port'][0]} with {new_alert['hits'][0]} hits—Raj says threat!")
else:
    print("Chill—Raj says safe.")
    
Run It: Command line,
type  === “python ai_shadow.py”

—watch it shadow your calls!
Bumps in the Road

Few Calls: 3 logs won’t cut it—aim for 50+.
Real Logs: Fake’s fine, but Splunk data’s gold.
Overfit: Might mimic me too hard—test it lots.

Why I Love It

It’s my analyst clone—saves time, shows my skills. World’s first, Raj-style!
