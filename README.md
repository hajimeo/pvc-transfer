# Process to copy contents from one PVC to another

I created this to allow me to migrate from different storage backends for a given project. The process would be:

 * Create a new PVC using the preferred storage backend
 * Shutdown app (scale replicas to zero)
 * Run sync process job
 * Edit Pod specs to use new PVC
 * Scale app back up

### Example
```
kubectl apply -f nfs-pv.yaml
kubectl apply -f local-pv.yaml 

export SRC_PVC=nfs-pv-claim
export DST_PVC=local-pv-claim
kubectl apply -f <(eval "echo \"$(cat pod-template.yaml)\"")

# Example after connecting to the pad with Shell
mkdir /dest/nxrm3
rsync ${RSYNC_OPTS:-"-apvH"} /srcd/ /dest/nxrm3/
```
NOTE: Need to be careful about quotes in xxxx-template.yaml files.