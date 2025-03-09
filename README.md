# Best Practices for OKE

TF scripts adapted from [FoggyKitchen.com](https://foggykitchen.com/)


To deploy OKE using this Module with minimal effort use this:

```hcl
module "fk-oke" {
  source                        = "github.com/mlinxfeld/terraform-oci-fk-oke"
  tenancy_ocid                  = var.tenancy_ocid      # Our tenancy OCID     
  compartment_ocid              = var.compartment_ocid  # Compartment OCID where OKE and network will be deployed
  cluster_type                  = "basic"               # Basic cluster
  use_existing_vcn              = false                 # Module itself will create all necessary network resources
  is_api_endpoint_subnet_public = true                  # OKE API Endpoint will be public (Internet facing)
  is_lb_subnet_public           = true                  # OKE LoadBalanacer will be public (Internet facing)
  is_nodepool_subnet_public     = true                  # OKE NodePool will be public (Internet facing)
}

```

Argument | Description
--- | ---
compartment_ocid | Compartment's OCID where OKE will be created
ssh_authorized_keys | Public SSH key to be included in the ~/.ssh/authorized_keys file for the default user on the instance
ssh_private_key | The private key to access instance
use_existing_vcn | If you want to inject already exisitng VCN then you need to set the value to TRUE.
use_existing_nsg | If you want to inject already exisitng NSG then you need to set the value to TRUE.
vcn_cidr | If use_existing_vcn is set to FALSE then you can define VCN CIDR block and then it will used to create VCN within the module.
vcn_id | If use_existing_vcn is set to TRUE then you can pass VCN OCID and module will use it to create OKE Cluster.
node_subnet_id | If use_existing_vcn is set to TRUE then you can pass NodePool Subnet OCID and module will use it to create OKE NodePool.
nodepool_subnet_cidr | If use_existing_vcn is set to FALSE then you can define NodePool CIDR block and then it will used to create NodePool within the module.
lb_subnet_id | If use_existing_vcn is set to TRUE then you can pass LoadBalancer Subnet OCID and module will use it to define service_lb_subnet_ids.
lb_subnet_cidr | If use_existing_vcn is set to FALSE then you can define LoadBalancer CIDR block and then it will used to create service_lb_subnet_ids within the module.
api_endpoint_subnet_id | If use_existing_vcn is set to TRUE then you can pass API EndPoint Subnet OCID and module will use it to define endpoint_config.
api_endpoint_subnet_cidr | If use_existing_vcn is set to FALSE then you can define API EndPoint CIDR block and then it will used to create endpoint_config within the module.
api_endpoint_nsg_ids | If use_existing_vcn is set to TRUE then you can pass API EndPoint Network Security Groups OCID and module will use it to define endpoint_config.
oci_vcn_ip_native | If you want to enable POD native networking (PODs associated with VCN/Subnet), then you need to turn the value to TRUE.
pod_subnet_id | If use_existing_vcn is set to TRUE and oci_vcn_ip_native is set to TRUE then you can pass POD Subnet OCID and module will associate it with each and every POD in OKE.
max_pods_per_node | If oci_vcn_ip_native is set to TRUE then you can define maximum value of PODs per OKE node.
oke_cluster_name | The name of the OKE Cluster.
vcn_native | if you want to use modern VCN-native mode for OKE then you need to set the value to TRUE.
is_api_endpoint_subnet_public | If vcn_native is set to TRUE then you can choose if API EndPoint will be in the public or private subnet.
is_lb_subnet_public | If vcn_native is set to TRUE then you can choose if LoadBalancer will be in the public or private subnet.
is_nodepool_subnet_public | If vcn_native is set to TRUE then you can choose if NodePool will be in the public or private subnet.
k8s_version | Version of K8S.
pool_name | Node Pool Name.
node_shape | Shape for the Node Pool members. 
node_ocpus | If node_shape is Flex then you can define OCPUS.
node_memory | If node_shape is Flex then you can define Memory.
node_linux_version | Node Oracle Linux Version.
node_count | Number of Nodes in the Pool.
pods_cidr | K8S PODs CIDR
services_cidr | K8S Services CIDR
cluster_options_add_ons_is_kubernetes_dashboard_enabled | If you want to set cluster_options_add_ons_is_kubernetes_dashboard_enabled to TRUE.
cluster_options_add_ons_is_tiller_enabled | If you want to use Tiller then you need to set the value to TRUE.
cluster_type | Default is **enhanced** may also be set to **basic**
node_pool_initial_node_labels_key | You can pass here node_pool_initial_node_labels_key.
node_pool_initial_node_labels_value | You can pass here node_pool_initial_node_labels_value.
node_eviction_node_pool_settings | If you want to setup Node Eviction Details configuration then set the value to TRUE (by default the value is equal to FALSE).
eviction_grace_duration | If node_eviction_node_pool_settings is set to TRUE then you can setup duration after which OKE will give up eviction of the pods on the node. PT0M will indicate you want to delete the node without cordon and drain. Default PT60M, Min PT0M, Max: PT60M. Format ISO 8601 e.g PT30M
is_force_delete_after_grace_duration | If node_eviction_node_pool_settings is set to TRUE then you can setup underlying compute instance to be deleted event if you cannot evict all the pods in grace period.
ssh_public_key | If you want to use your own SSH public key instead of generated onne by the module.

## Contributing
This project is open source. Please submit your contributions by forking this repository and submitting a pull request! [FoggyKitchen.com](https://foggykitchen.com/) appreciates any contributions that are made by the open source community.

## License
Copyright (c) 2025 [FoggyKitchen.com](https://foggykitchen.com/)

Licensed under the Universal Permissive License (UPL), Version 1.0.

See [LICENSE](LICENSE) for more details.
