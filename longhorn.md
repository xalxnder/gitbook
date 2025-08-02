# Longhorn

### PVC Stuck In Detaching/ Attaching Loop

When checking longhorn, I noticed a PVC constantly switching between Attaching and Detaching. The pod that this was related to was a vm-single pod in my victoria-metrics-k8s-stack namespace. After checking the events, I saw the following error



```bash
volume pvc-2221ff51-3872-4f7c-9340-cbb6fd9bb97f failed to attach to node r10-lab-w2 with attachmentID cs │
│ i-c0cdaf4a450afddd51a9e35bb7cbcf9190f89c1bd4ba35ec71d317ff5853e8b3
```



#### What was my actual issue?

From what i could tell, I had a ton of left over volume attachments (`volumeattachments.longhorn.io`).  I'm still unsure of what happened, and why these were leftover but  I resolved by:

1. Disabling auto-sync for the particular app
2. Cleaning up any volumeattachments.longhorn.io that were in an errored state.
3. Deleting anything relating to the `pvc-2221ff51` stuck in the loop. After syncing, a new PVC was created, and it was able to attach successfully .&#x20;
