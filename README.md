# Endgame Virtual Machine(s)

The Endgame ISO (EndGame-3.20.0-8606.01fc7390.ga-324.iso), provided by customer boots into a menu with various install options.

1. SMP Platform > Automated Install
2. MCM Server > Automated Install
3. Advanced > SMP Platform (Text)
4. CentOS > Install CentOS 7

## Recreate Virtual Machines (using Kubevirt/CDI)

Prerequisites: Cluster with Kubevirt, CDI, and Baffles-UI installed

1. Upload iso using CDI. i.e.
  ```
  kubectl port-forward -n cdi service/cdi-uploadproxy 18443:443
  virtctl image-upload pvc endgame-iso --image-path=EndGame-3.20.0-8606.01fc7390.ga-324.iso --access-mode=ReadWriteOnce --pvc-size=3G --uploadproxy-url=https://localhost:18443 --insecure
  ```
2. `kubectl apply -k manifests/kustomization.yaml`
3. Using Baffles (or a VNC viewer) manually select install option. 
   1. Install is performed automatically after initial selection
4. On next boot, Installed application prompts for login credentials (which are unknown as of this documentation)

