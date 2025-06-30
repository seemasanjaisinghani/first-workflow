kubectl create deployment demo --image=httpd --port=80
kubectl expose deployment demo --port=80 --target-port=80

Create Ingress File -
ingress.yaml with below content :
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: demo-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: demo.local
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: demo
            port:
              number: 80
