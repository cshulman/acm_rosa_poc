# IMPORT EXISTING CLUSTER for management:

### Prereq (optional) on hub:
- Create ManagedClusterSet to group ManagedClusters 
```oc create -f import_spoke/hub/managedclusterset-rosa.yaml```
----

## HUB/ACM cluster steps:

- Create ManagedCluster 
```oc create -f import_spoke/hub/<cluster-name>-managedcluster.yaml```

- Create KlusterletAddonConfig for ManagedCluster
```oc create -f import_spoke/hub/<cluster-name>-klusterletaddon.yaml```

- Extract klusterlet crd & import from secret in the ManagedCluster ns


```oc get secret <cluster-name>-import -n <cluster-name> -o jsonpath={.data.crds\\.yaml} | base64 --decode > import_spoke/spoke/<cluster-name>-klusterlet-crd.yaml```

```oc get secret <cluster-name>-import -n <cluster-name> -o jsonpath={.data.import\\.yaml} | base64 --decode > import_spoke/spoke/<cluster-name>-import.yaml```

----

## SPOKE:

- Create Klusterlet crd
```oc create -f import_spoke/spoke/<cluster-name>-klusterlet-crd.yaml```

- Create all resources from import file
```oc create -f import_spoke/spoke/<cluster-name>-import.yaml```
