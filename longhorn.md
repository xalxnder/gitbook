# Longhorn

### PVC Stuck In Detaching/ Attaching Loop

1. Che

#### What was my actual issue?

From what i could tell, i had a ton of left over volume attachments.  I resolved by disabling autosync for the particular app, then deleting anything releating to the PVC stuck in the loop. After sycing, my PVC was able to successfully attach.&#x20;
