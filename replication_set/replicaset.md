# ReplicaSet requires selector section
ReplicaSet can manage pods that have been created before the creation of replicaSet.
selector.matchLabels will be used to retrieve pods.

# scale replicaset
kubectl scale --replicas=6 replicaset myapp-replicaset