**Platform:** LetsDefend

**Module:** SOC140 - Phishing Mail Detected - Suspicious task Scheduler

**Difficulty:** Easy

**Target:** mark@letsdefend.io 

**Date:** 2026-06-13

---

<h3 align =center> Walkthrough </h3>

***Alert Review:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The very first thing you want to do is expand the alert and read every single field before jumping into the investigation.
<br>
<br>

<img width="1261" height="474" alt="p-1" src="https://github.com/user-attachments/assets/320ffc0e-3f15-4bee-a7c3-a09e4d9faf08" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; This alert is EventID 82, triggered on March 21, 2021 at 12:26 PM, under the rule SOC140 - Phishing Mail Detected - Suspicious Task Scheduler. That Device Action field is the first important thing to note here. Unlike a proxy alert where Allowed means the connection went through, here the email was Blocked — meaning it never reached the recipient.
<br>
<br>

---
***Starting the Playbook:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The first playbook step is parse Email, which is sking you to gather all the key information about the incoming email before doing any analysis.
<br>
<br>
</b>

<img width="598" height="336" alt="p-2" src="https://github.com/user-attachments/assets/b249ae2a-674b-480e-a979-66708443e191" />

<br>
<br>

- When was it sent? -> Mar 21, 2021, 12:26 PM

- What is the email's SMTP address? -> 189.162.189.159

- what is the sender address? -> aaronluo@cmail.carleton.ca

- what is the recipient address? -> mark@letsdefend.io

- Is the mail content suspicious? -> yes

- Are there any attachment? -> yes

&nbsp;&nbsp;&nbsp;&nbsp; You should never skip straight to analysis without first fully understanding what you're looking at.
<br>

---
***Examining the Email:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The playbook asks whether the email contains attachments or URLs.
<br>
<br>

<img width="606" height="335" alt="p-3" src="https://github.com/user-attachments/assets/e10aac0b-0236-4bba-b794-c98afcac169b" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; So, let's head over to Email Security and pull up the email.
<br>
<br>

<img width="1280" height="649" alt="p-4" src="https://github.com/user-attachments/assets/0fb14e50-3279-4b39-971d-62566ff2a364" />

<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; There is also an attachment with the hash 72c812cf21909a48eb9cceb9e04b865d. The attachment is password-protected with the password "infected" written right there in the email body itself. The answer is clearly Yes.
<br>
<br>

---
***Attachment Analysis:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The playbook directs you to analyze the URL or attachment using third-party tools.
<br>
<br>
