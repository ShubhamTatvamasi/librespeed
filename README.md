# librespeed

Deploy on Kubernetes:
```bash
kubectl run librespeed --image=linuxserver/librespeed --port=80 --expose

kubectl patch svc librespeed \
  --patch='{"spec": {"type": "NodePort"}}'

kubectl patch svc librespeed \
  --patch='{"spec": {"ports": [{"nodePort": 30333, "port": 80}]}}'
```
