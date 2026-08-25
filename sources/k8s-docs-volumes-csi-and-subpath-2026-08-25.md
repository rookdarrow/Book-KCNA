---
source_url: "https://kubernetes.io/docs/concepts/storage/volumes/#csi"
fetched_at: "2026-08-25T02:34:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "csi-driver", "csi-migration", "in-tree-volume-plugin", "fourth-pluggable-interface", "subpath", "subpath-no-updates", "emptydir-size-limit"]
---
# Volumes — CSI, subPath and out-of-tree plugins (kubernetes.io/docs/concepts/storage/volumes/)

CLOSES arc-outline blocking gap G11. Retrieved from the page's Markdown source in
the kubernetes/website repository, so the wording below is the docs' own.

## csi

"Container Storage Interface (CSI) defines a standard interface for container orchestration systems (like Kubernetes) to expose arbitrary storage systems to their container workloads."

Note: "Support for CSI spec versions 0.2 and 0.3 is deprecated in Kubernetes v1.13 and will be removed in a future release."

Note: "CSI drivers may not be compatible across all Kubernetes releases. Please check the specific CSI driver's documentation for supported deployment steps for each Kubernetes release and a compatibility matrix."

"Once a CSI-compatible volume driver is deployed on a Kubernetes cluster, users may use the `csi` volume type to attach or mount the volumes exposed by the CSI driver."

"A `csi` volume can be used in a Pod in three different ways:

* through a reference to a PersistentVolumeClaim
* with a generic ephemeral volume
* with a CSI ephemeral volume if the driver supports that"

"The following fields are available to storage administrators to configure a CSI persistent volume:"

* "`driver`: A string value that specifies the name of the volume driver to use. This value must correspond to the value returned in the `GetPluginInfoResponse` by the CSI driver as defined in the CSI spec. It is used by Kubernetes to identify which CSI driver to call out to, and by CSI driver components to identify which PV objects belong to the CSI driver."
* "`volumeHandle`: A string value that uniquely identifies the volume. This value must correspond to the value returned in the `volume.id` field of the `CreateVolumeResponse` by the CSI driver as defined in the CSI spec. The value is passed as `volume_id` in all calls to the CSI volume driver when referencing the volume."
* "`readOnly`: An optional boolean value indicating whether the volume is to be 'ControllerPublished' (attached) as read-only. Default is false. This value is passed to the CSI driver via the `readonly` field in the `ControllerPublishVolumeRequest`."
* "`fsType`: If the PV's `VolumeMode` is `Filesystem`, then this field may be used to specify the filesystem that should be used to mount the volume. If the volume has not been formatted and formatting is supported, this value will be used to format the volume."
* "`volumeAttributes`: A map of string to string that specifies static properties of a volume. This map must correspond to the map returned in the `volume.attributes` field of the `CreateVolumeResponse` by the CSI driver as defined in the CSI spec."
* "`controllerPublishSecretRef`: A reference to the secret object containing sensitive information to pass to the CSI driver to complete the CSI `ControllerPublishVolume` and `ControllerUnpublishVolume` calls. This field is optional, and may be empty if no secret is required."
* "`nodeExpandSecretRef`: A reference to the secret containing sensitive information to pass to the CSI driver to complete the CSI `NodeExpandVolume` call. This field is optional and may be empty if no secret is required."
* "`nodePublishSecretRef`: A reference to the secret object containing sensitive information to pass to the CSI driver to complete the CSI `NodePublishVolume` call. This field is optional and may be empty if no secret is required."
* "`nodeStageSecretRef`: A reference to the secret object containing sensitive information to pass to the CSI driver to complete the CSI `NodeStageVolume` call. This field is optional and may be empty if no secret is required."

### CSI raw block volume support

"Vendors with external CSI drivers can implement raw block volume support in Kubernetes workloads."

"You can set up your PersistentVolume/PersistentVolumeClaim with raw block volume support as usual, without any CSI-specific changes."

### CSI ephemeral volumes

"You can directly configure CSI volumes within the Pod specification. Volumes specified in this way are ephemeral and do not persist across Pod restarts."

### Windows CSI proxy

"CSI node plugins need to perform various privileged operations like scanning of disk devices and mounting of file systems. These operations differ for each host operating system. For Linux worker nodes, containerized CSI node plugins are typically deployed as privileged containers. For Windows worker nodes, privileged operations for containerized CSI node plugins are supported using csi-proxy, a community-managed, stand-alone binary that needs to be pre-installed on each Windows node."

### Migrating to CSI drivers from in-tree plugins

"The `CSIMigration` feature directs operations against existing in-tree plugins to corresponding CSI plugins (which are expected to be installed and configured). As a result, operators do not have to make any configuration changes to existing Storage Classes, PersistentVolumes, or PersistentVolumeClaims (referring to in-tree plugins) when transitioning to a CSI driver that supersedes an in-tree plugin."

Note: "Existing PVs created by an in-tree volume plugin can still be used in the future without any configuration changes, even after the migration to CSI is completed for that volume type, and even after you upgrade to a version of Kubernetes that doesn't have compiled-in support for that kind of storage."

"As part of that migration, you - or another cluster administrator - must have installed and configured the appropriate CSI driver for that storage. The core of Kubernetes does not install that software for you."

"After that migration, you can also define new PVCs and PVs that refer to the legacy, built-in storage integrations. Provided you have the appropriate CSI driver installed and configured, the PV creation continues to work, even for brand-new volumes. The actual storage management now happens through the CSI driver."

"The operations and features that are supported include: provisioning/delete, attach/detach, mount/unmount, and resizing of volumes."

## Using subPath

CLOSES the outline's "partial fifth" gap: subPath as a general mechanism, not only
its no-updates exception.

"Sometimes, it is useful to share one volume for multiple uses in a single Pod. The `volumeMounts[*].subPath` property specifies a sub-path inside the referenced volume instead of its root."

"The following example shows how to configure a Pod with a LAMP stack (Linux, Apache, MySQL, PHP) using a single, shared volume. This sample `subPath` configuration is not recommended for production use."

"The PHP application's code and assets map to the volume's `html` folder and the MySQL database is stored in the volume's `mysql` folder. For example:"

    apiVersion: v1
    kind: Pod
    metadata:
      name: my-lamp-site
    spec:
        containers:
        - name: mysql
          image: mysql
          env:
          - name: MYSQL_ROOT_PASSWORD
            value: "rootpasswd"
          volumeMounts:
          - mountPath: /var/lib/mysql
            name: site-data
            subPath: mysql
        - name: php
          image: php:7.0-apache
          volumeMounts:
          - mountPath: /var/www/html
            name: site-data
            subPath: html
        volumes:
        - name: site-data
          persistentVolumeClaim:
            claimName: my-lamp-site-data

### Using subPath with expanded environment variables

"Use the `subPathExpr` field to construct `subPath` directory names from downward API environment variables. The `subPath` and `subPathExpr` properties are mutually exclusive."

## Resources

"The storage medium (such as Disk or SSD) of an `emptyDir` volume is determined by the medium of the filesystem holding the kubelet root dir (typically `/var/lib/kubelet`). There is no limit on how much space an `emptyDir` or `hostPath` volume can consume, and no isolation between containers or Pods."

## Out-of-tree volume plugins

"The out-of-tree volume plugins include Container Storage Interface (CSI), and also FlexVolume (which is deprecated). These plugins enable storage vendors to create custom storage plugins without adding their plugin source code to the Kubernetes repository."

"Previously, all volume plugins were 'in-tree'. The 'in-tree' plugins were built, linked, compiled, and shipped with the core Kubernetes binaries. This meant that adding a new storage system to Kubernetes (a volume plugin) required checking code into the core Kubernetes code repository."

"Both CSI and FlexVolume allow volume plugins to be developed independently of the Kubernetes code base, and deployed (installed) on Kubernetes clusters as extensions."

### flexVolume (deprecated)

"FlexVolume is an out-of-tree plugin interface that uses an exec-based model to interface with storage drivers. The FlexVolume driver binaries must be installed in a pre-defined volume plugin path on each node, and in some cases, the control plane nodes as well."

Note: "FlexVolume is deprecated. Using an out-of-tree CSI driver is the recommended way to integrate external storage with Kubernetes."
