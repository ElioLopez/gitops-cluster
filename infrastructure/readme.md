## create sealed secrets

for synology CSI driver
more info on: https://github.com/bitnami-labs/sealed-secrets
```
kubectl create secret generic synology-csi \
--from-literal=k8s_user=XXXXXXX \
--from-literal=k8s_pass=XXXXXXXXXXX \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
--controller-name sealed-secrets \
-n kube-system  >  synology-csi-sealed-secrets.yml
```

username: svc-k8s
password: jzMM3DNTA4Pqcdwrc_J98A.J2E0M-zMygEYfewm



echo -n <my-secret> | kubeseal --controller-name=sealed-secrets --raw --from-file=/dev/stdin --scope=namespace-wide


echo -n svc-k8s | kubeseal --controller-name=sealed-secrets --raw --from-file=/dev/stdin --scope=namespace-wide
AgBS3D315mVgMo9VVXGaXV8dVPfVe4OHqfuekHG5u3kHklqbn6lVibzXYLZVEJFV3FaOpB0iRg8Ak9Qn3DjYMjsNRgh7g+kWHvPEn/Mf/bMpKMIPnAxxLZalQ0ZHebKJ86mwaF9zZjdmOJ3rTYY2c0SHl41kSw3XkBf0IRym+REW/8qSm0Cre5YiyzWSt035zzX1xmhJxesE/+FsEIEryo+g9swm25/yCd8pY/Ek1CWS3L3RCy/CkZ6UV3o4VXddgCYTNN1S8Vd9CjhwI2wpvgGH4LHO2i+B9bfY/qBXHyYEMihu7AC9JBQr81taLk02UY+3VlLUSwZgVr/SxhARcQKm7j6UtKQOh6YXXAvlegdzwE5iZ9U/bbJDS7CMVbGBVLZIE6uyeHvRVmC7otpBgCL211QCIVkxAAPliq0fEq85RxNKTR33WRrLnYDKKnSlDJl6FqswtyeMRp2FsI+XBR6rKw8euU5ZDd1zBW+dUqx3qHAM9Hll4AdcckFsE9a9EmhCmK01IpclxTIYdz/KfY5go6iXMcnJlKwg5mUhEIz1KCUgPn2IFQ0xWGHtUEtO/mNYyaeLFmM8B0SO6Iw0JD7UzcNtEGh+JriIypEHzS/yR4KQbG8TZgF1GEZEqwIkpQP3M83JYxkzha0QwJaTugW8Wa9tZDtgnjj2lf5jROnmAo+i5qlvRZK2vfH/X/AThezZXn7pU7bU


echo -n jzMM3DNTA4Pqcdwrc_J98A.J2E0M-zMygEYfewm | kubeseal --controller-name=sealed-secrets --raw --from-file=/dev/stdin --scope=namespace-wide
AgAiPlXop2WIGg05j7WQg6SnF2tQTKTMEesnAAGYbEVhWm4zUuGVCTQiPcwsprTGuf4srk33vHKw9cjR1D+LVAb1WmOZTCBWfUjb/71lY+MEXHTOdjnhkDEGsquuwocqc0GAYTXRoJ3GxLskoLxpHztA5uAN1ZcvZEClAsAIWoiWUogPlx497l1OAle7wJnPT4V4Lsm1W+wFS2J0fpktWf8hF/bC/S0liHwXeAAznEKoV7MzLl+ElRv+micK6dH+aXAeRkvVIGQB6ChB5xyn2JB9CX5RhlQ22RjBzBPAT37PrO3vqKb8XkIvCWC5I4sH5cEnMv6N87FiLtkndllTJeJE5aCXnbFN1XfzOKRj0GbGxKuP3wdA1+UZqmzK0mqauYLirexinRYIln2ibRzssy1jCGly5BFmh2uOG6CojkBjxYtsMlZCOYNfTR/Ac9D59CuOXNxnyS+O+JEBwckQMei+CZ4JdxRadGTl4iiJ+yLK0AyXdCW1n+fDMmzBwZR/WlwHoeUWw65EXZ0lfBCbxkNQioxAspR4b7wlJgwHf/c0EwnBlqGV+ChPIeqi2BkmsoN2JEX3zlW/CSp0jJxlMTEMrztTeeWcx2IqBzv+UihGValxlvYxa6WS5V75zH83tXZ1qDXEZ1CH2RFFVuzSsYRZSw1xFivZQt1cbwFSWnojajQ2TLZGcfd8s2NaQM+KdTc1QBDusXlX4jw8wgbijByphBUQyG+/65k35uh57TMjebZzrEqpaV8=