# The Code

```java
for (int i = 0; i < 2; ++i) {
    HashMap<TaskAttemptId, Container> taskSet = i == 0 ? assignedRequests.maps
        : assignedRequests.reduces;
    // kill running containers
    for (Map.Entry<TaskAttemptId, Container> entry : taskSet.entrySet()) {
        TaskAttemptId tid = entry.getKey();
        NodeId taskAttemptNodeId = entry.getValue().getNodeId();
        if (unusableNodes.contains(taskAttemptNodeId)) {
        LOG.info("Killing taskAttempt:" + tid
            + " because it is running on unusable node:"
            + taskAttemptNodeId);
        // If map, reschedule next task attempt.
        boolean rescheduleNextAttempt = (i == 0) ? true : false;
        eventHandler.handle(new TaskAttemptKillEvent(tid,
            "TaskAttempt killed because it ran on unusable node"
                + taskAttemptNodeId, rescheduleNextAttempt));
        }
    }
}
```
