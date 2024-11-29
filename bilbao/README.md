# Description
There's a Kubernetes Deployment with an Nginx pod and a Load Balancer declared in the manifest.yml file. The pod is not coming up. Fix it so that you can access the Nginx container through the Load Balancer.

## Process
Check the error.
```
admin@i-0ca1266c85a416e7b:~$ curl 10.43.216.196
curl: (7) Failed to connect to 10.43.216.196 port 80: Connection refused
```

Error on the Pod manifest.
```
  Warning  FailedScheduling  316d  default-scheduler  0/2 nodes are available: 1 node(s) didn't match Pod's node affinity/selector, 1 node(s) had untolerated taint {node.kubernetes.io/unreachable: }. preemption: 0/2 nodes are available: 2 Preemption is not helpful for scheduling..
```

Nodes.
```
admin@i-0ca1266c85a416e7b:~$ kubectl get nodes
NAME                  STATUS     ROLES                  AGE    VERSION
node1                 Ready      control-plane,master   316d   v1.28.5+k3s1
i-02f8e6680f7d5e616   NotReady   control-plane,master   316d   v1.28.5+k3s1
```

Label nodes.
```
admin@i-0ca1266c85a416e7b:~$ kubectl label nodes node1 disk=ssd
node/node1 labeled
```

Delete existing pod.
```
admin@i-0ca1266c85a416e7b:~$ kubectl delete pod nginx-deployment-67699598cc-zrj6f
pod "nginx-deployment-67699598cc-zrj6f" deleted
```

Different error on the Pod manifest.
```
Warning  FailedScheduling  38s   default-scheduler  0/2 nodes are available: 1 Insufficient memory, 1 node(s) had untolerated taint {node.kubernetes.io/unreachable: }. preemption: 0/2 nodes are available: 1 No preemption victims found for incoming pod, 1 Preemption is not helpful for scheduling..
```

Reduce memory request in manifest and delete pod.
```
admin@i-0ca1266c85a416e7b:~$ kubectl delete pod nginx-deployment-67699598cc-92v59
pod "nginx-deployment-67699598cc-92v59" deleted
```

New pod is OK
```
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  47s   default-scheduler  Successfully assigned default/nginx-deployment-84bbfc9fb5-9ljql to node1
  Normal  Pulling    46s   kubelet            Pulling image "localhost:5000/nginx"
  Normal  Pulled     35s   kubelet            Successfully pulled image "localhost:5000/nginx" in 11.626s (11.626s including waiting)
  Normal  Created    35s   kubelet            Created container nginx
  Normal  Started    34s   kubelet            Started container nginx
  ```
