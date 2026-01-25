```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: rubesh-adapter
spec:
  volumes:
    - name: config-volume
      emptyDir: {}

  containers:
  - name: app
    image: busybox:1.36.1
    args:
      - /bin/sh
      - -c
      - >
        while true;
        do
          echo "$(date) | $(du -sh ~)" >> /var/logs/resource-usage.txt;
          sleep 5;
        done;
    volumeMounts:
      - name: config-volume
        mountPath: /var/logs
    resources: {}

  - name: transformer
    image: busybox:1.36.1
    args:
      - /bin/sh
      - -c
      - >
        sleep 20;
        while true;
        do
          while read LINE;
          do
            echo "$LINE" | cut -f2 -d"|" >> /var/logs/processed-usage.txt;
          done < /var/logs/resource-usage.txt;
          sleep 20;
        done;
    volumeMounts:
      - name: config-volume
        mountPath: /var/logs

  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
$ kubectl apply -f rubesh-adapter.yaml
$ kubectl exec rubesh-adapter --container=transformer -it -- /bin/sh
# cat /var/logs/processed-usage.txt
/ # cat /var/logs/processed-usage.txt
 4.0K   /root
 4.0K   /root
 4.0K   /root
 4.0K   /root
 4.0K   /root
 4.0K   /root
# exit
```
