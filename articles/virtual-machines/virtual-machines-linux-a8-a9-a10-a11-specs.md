<properties
 pageTitle="About A8, A9, A10, A11 VM sizes with Linux | Microsoft Azure"
 description="Get background information and considerations for using the Azure A8, A9, A10, and A11 compute-intensive sizes for Linux VMs"
 services="virtual-machines-linux"
 documentationCenter=""
 authors="dlepow"
 manager="timlt"
 editor=""
 tags="azure-resource-manager,azure-service-management"/>
<tags
ms.service="virtual-machines-linux"
 ms.devlang="na"
 ms.topic="article"
 ms.tgt_pltfrm="vm-linux"
 ms.workload="infrastructure-services"
 ms.date="08/04/2016"
 ms.author="danlep"/>

# About the A8, A9, A10, and A11 compute-intensive instances 

Here is background information and some considerations for using the Azure A8, A9, A10, and A11 instances, also known as *compute-intensive* instances. This article focuses on using these instances for Linux VMs. This article is also available for [Windows VMs](virtual-machines-windows-a8-a9-a10-a11-specs.md).

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

[AZURE.INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## Access to the RDMA network

Within a single cloud service or an availability set, clusters of size A8 and A9 Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation can access the RDMA network in Azure to run Linux MPI applications. See [Set up a Linux RDMA cluster to run MPI applications](virtual-machines-linux-classic-rdma-cluster.md) for deployment options and sample configuration steps.

* **Distributions** - SUSE Linux Enterprise Server (SLES) 12 for HPC, SLES 12 for HPC (Premium), CentOS-based 7.1 HPC, or CentOS-based 6.5 HPC, deployed from an Azure Marketplace image

* **MPI** - Intel MPI Library 5.x

    >[AZURE.NOTE] Intel MPI 5.1 is already installed on the CentOS-based HPC images in the Marketplace. To use Intel MPI on SLES 12 SP1 HPC VMs, you must separately install it, the packages are provided in /opt/intelMPI/intel_mpi_packages/, see [HPC Update for Azure…Finally](https://www.suse.com/communities/blog/hpc-update-azure-finally/) for details.

Currently, Azure Linux RDMA drivers are only installed when you deploy RDMA-enabled SLES 12 SP1 or higher HPC and CentOS HPC images from the Azure Marketplace. You can't install the drivers on other Linux VMs you deploy.

>[AZURE.NOTE]On the CentOS-based HPC images from the Marketplace, kernel updates are disabled in the **yum** configuration file. This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated. SLES based HPC images are set up such that kernel updates are possible.


## Considerations for HPC Pack and Linux

[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx) is Microsoft’s free HPC cluster and job management solution. The latest releases of HPC Pack 2012 R2 support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node. Linux compute nodes deployed on A8 or A9 VMs and running a supported MPI implementation can run MPI applications that access the RDMA network. To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](virtual-machines-linux-classic-hpcpack-cluster.md).

## Network topology considerations

* On size A8 or A9 Linux VMs in Azure, Eth1 is reserved for RDMA network traffic. Do not change any Eth1 settings or any information in the configuration file referring to this network. Eth0 is reserved for regular Azure network traffic.

* In Azure IP over Infiniband (IB) is not supported. Only RDMA over IB is supported.


## Next steps

* For details about availability and pricing of the A8, A9, A10, and A11 instances, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).

* For storage capacities and disk details, see [Sizes for virtual machines](virtual-machines-linux-sizes.md).

* To get started deploying and using A8 and A9 instances with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](virtual-machines-linux-classic-rdma-cluster.md).


