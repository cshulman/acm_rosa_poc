# INSTALL ACM 

**Create ns, og & sub for ACM**
```oc create -f install/open-cluster-management-install.yaml```

**Create multiclusterhub**
    aka mch - which creates mce etc. + adds local-cluster as managed by mce/acm
```oc create -f install/multi-clusterhub.yaml```
