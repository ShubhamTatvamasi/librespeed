# librespeed

create deployment and service:
```bash
kubectl create deployment librespeed --image=linuxserver/librespeed
kubectl expose deployment librespeed --port=80 --name=librespeed
```

delete deployment and service:
```bash
kubectl delete deploy/librespeed svc/librespeed ing/librespeed
```

Deploy on Kubernetes:
```bash
kubectl run librespeed --image=linuxserver/librespeed --port=80 --expose

kubectl patch svc librespeed \
  --patch='{"spec": {"type": "NodePort"}}'

kubectl patch svc librespeed \
  --patch='{"spec": {"ports": [{"nodePort": 30333, "port": 80}]}}'
```
> If using NodePort: http://k8s.shubhamtatvamasi.com:30333

Ingress value for librespeed
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: librespeed
spec:
  tls:
    - hosts:
      - librespeed.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: librespeed.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: librespeed
            servicePort: 80
EOF
```

