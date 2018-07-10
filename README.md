# CernVM-FS CSI driver

Currently supports only Kubernetes 1.10+

## Using in a container

### Storage Class
A storage class must be created that links to the CVMFS CSI.  
Use `provisioner: csi-cvmfsplugin`.

#### StorageClass parameters
Parameters must be provided for CVMFS to know what repository to access, and how.
```yaml
...
parameters:
  repository: example.repo.ch # mandatory, CVMFS repository address
  proxy: 0.123.123.123:3128 # mandatory, HTTP Proxy to access repository. 'DIRECT' for none.
  tag: # optional, defaults to `trunk`
  hash: # optional
...
```
Specifying both `tag` and `hash` is not allowed.

### Persistent Volume Claim
A persistent volume claim can then use the storage class you have created to dynamically provision a CVMFS volume.

### Application
Mount the persistent volume claim into your application as a volume, and then you can utlize it as a read-only file system.



## CSI Deployment to Cluster

Deploy `external-attacher`, `external-provisioner`, `driver-registrar` sidecar containers and the `csi-cvmfsplugin`:

```bash
$ ./deploy/kubernetes/csi-deploy.sh
```

Create the csi-cvmfs storage class, PVC and a Pod for testing:

```bash
$ ./deploy/kubernetes/user-deploy.sh
```
or
```bash
$ helm install /deploy/helm
```