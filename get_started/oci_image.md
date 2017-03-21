# Get Started with OCI Image Spec

Since version 0.8, hyperd supported [OCI Image](https://github.com/opencontainers/image-spec). You may save your images to OCI image format with [save](../reference/save.md) command, and load OCI Image with [load](../reference/load.md) command.

Here is a simple example:

```
# hyperctl images
REPOSITORY          TAG                 IMAGE ID     
busybox            latest                7968321274dc    
centos              7                   980e0e4c79ec  

//save centos:7 image as refname "hello" and busybox:latest image as refname "world" in mix-oci.tar usging oci image format
# hyperctl save -o /tmp/mix-oci.tar -f oci -r centos:7=hello -r busybox:latest=world centos:7 busybox:latest

// untar mix-oci.tar and find index.json file
# cat index.json |jq
{
  "schemaVersion": 2,
  "manifests": [
    {
      "mediaType": "application/vnd.oci.image.manifest.v1+json",
      "digest": "sha256:351c1c2957c21a76d7b74e94afabd6429d4a3d16cbe6ee7e7b1f351e39125490",
      "size": 346,
      "annotations": {
        "org.opencontainers.ref.name": "hello"
      },
      "platform": {
        "architecture": "amd64",
        "os": "linux"
      }
    },
    {
      "mediaType": "application/vnd.oci.image.manifest.v1+json",
      "digest": "sha256:87fe700a194b98ab383582f9981539d9a69d49e1143e91fe0e75c4a92f5de42e",
      "size": 344,
      "annotations": {
        "org.opencontainers.ref.name": "world"
      },
      "platform": {
        "architecture": "amd64",
        "os": "linux"
      }
    }
  ]
}

// rm centos:7 and busybox:latest images for loading them from mix-oci.tar
# hyperctl rmi centos:7 busybox:latest

// load centos and busybox images from mix-oci.tar and retag them as centos:test and busybox:test
# hyperctl load -i /tmp/oci/mix-oci.tar -r centos:7=hello -r busybox:test=world

# hyperctl images
REPOSITORY          TAG                 IMAGE ID     
busybox           test                7968321274dc    
centos              test                   980e0e4c79ec
```
