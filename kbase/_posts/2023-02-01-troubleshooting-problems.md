---
layout: post
title: Troubleshooting Technical Problems
description: >
  Where to start troubleshooting technical problems when you're just starting out.
categories: [kbase]
tags:       [multi-os, sysops]
---
1. this ordered seed list will be replaced by the toc
{:toc}

## Purpose
When you're just starting out in a technical role, it can be hard to know where to start troubleshooting problems. The following post summarizes an approach to technical troubleshooting for those new to the field or as a refresher for the more experienced.  
As more experience is gained, many of these steps will become intuition and additional steps can be added to suit the specific problem.

## Assumptions
+ This is just a starting point. Use what works and add as you see fit.
+ The below steps are aimed at troubleshooting from an operations perspective. Whilst development (programming) mirrors many of the steps, there are differences that would make the guide difficult to follow if it catered for both.
+ Troubleshooting a bug is different from investigating a new feature. This guide assumes that the problematic system is not doing something that it was intended to do.

## Background
When troubleshooting a technical problem, there are a few things that will serve you well:
+ **Curiosity** - The job will be far easier if you treat every problem like a puzzle that you want to solve. Solving problems is fundamental in developing more advanced skills and in many cases the things you learn whilst solving a problem can be transferred or adapted to new and exciting problems in the future!
+ **Initiative** - Try solving the problem first before you look up the answer. Copy/pasting the commands from a web page might get the job done but it rarely builds the skills to approach new problems that don't have an obvious answer in your search engine of choice.
+ **An understanding of the target system** - If you don't know how the system is supposed to work and how to interact with it, correcting the problem becomes much harder. Make a point of learning the systems that you will be responsible for maintaining. 

## Procedure
1. **Understand the Problem**  
The first step to fixing a problem is understanding what it actually is. If a problem is brought to you and it is unclear what is actually occurring, ask for more information. Without a clear understanding of the problem, there is no way to know if it has been fixed.  
For example, if you are told that "The printer isn't working", you are going to need more information. What exactly happens when someone tries to print? Can they select the printer from the print dialog? Do they successfully submit the print dialog but nothing comes out? Is the problem isolated to one user, or is everyone having the issue?  
You need to build up a clear picture of the problem before taking a guess.
2. **Recreate the Problem**  
Once you know what the problem is, can you recreate it? Recreating the problem allows you to test any potential fixes you apply. There are times when recreating the problem isn't possible because the issue is transient or there is a significant time cost required to get the system into the problem state. However, where possible recreating the problem will aid in testing the solution. It should be noted that recreating the problem can be as simple as observing the continuing issue on the effected system. It does not always have to be recreated separately.
3. **Start from the beginning**  
When attempting to determine the cause, work through the system from the beginning. It is often tempting to jump right into the middle but that often results in simple errors being missed. If a process relies on the internet, is an Ethernet cable plugged in? Is the laptop connected to WiFi? Can you load a webpage?
4. **Check the Logs**  
Most software logs errors somewhere. This may be to a file, built into the operating system, or displayed in the interface. Know where to go to find the relevant logs. You may need to check the logging path in a configuration file, by reading the software documentation, or by doing a quick search on the internet. Once you know how to inspect the logs, look through them for any errors and if the solution is obvious, skip the next step and continue the process. If you're unsure, note down what the error is and move to the next step.
5. **Search**  
If you're unsure what an error means, search for an explanation. In some cases, the product documentation will list common errors and solutions. In other cases, a search on the internet may be in order. If searching on the internet, be sure to understand the presented solution before you blindly follow the advice. If you're unsure what the solution is advising, be curious and look further into the steps presented. The error may turn out to be unrelated to this problem which will mean looping back to the previous step but if you find something that could be the cause, continue on to the next step.
6. **Test the Solution**  
Once you have found a potential solution it's time to try fixing the affected system. At this stage, it becomes obvious why step 2 exists. After implementing the fix, the problem should not reoccur when attempting to recreate it. If the problem persists you will need to loop back to an earlier step (possibly 3, 4, or 5) and keep trying to find a solution. Be sure to also revert any changes you made if you suspect they may cause additional issues in future. In the event that you've exhausted all of the solutions and your not sure where to go from here, move on to the next step.
7. **Ask for Help**  
There is a point where you need to bring in someone with more experience to help you out. If you've worked through the problem and can explain what you've already tried, the person you ask will usually be happy to help out. Asking for help can be from a more experienced co-worker, posting to a relevant forum or chat group, or by outsourcing to a third party. The key to getting useful help is to explain the problem clearly and in its entirety and to detail the steps you've tried to resolve the issue on your own. When you do get the solution, be sure to have it explained to you so that you can learn from it. In the event that you encounter a similar problem in the future, you will be better equipped to deal with it.

## Conclusion
Coming up against new problems can be daunting and stressful, especially when you're just starting out. The guide posted here is an effort to provide a framework from which to start and build on. With the fundamentals covered, you can begin to enjoy the process of fixing and learn to tackle more complex problems.