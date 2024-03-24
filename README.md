# Bare metal Kubernetes with MAAS, LXD, and Juju

## Intro

This is a series of commands and configuration files that will guide you to build your own emulated bare metal k8s cluster on a single machine, using <https://maas.io>.

It is designed to be used in conjunction with an explanatory video tutorial: <https://www.youtube.com/watch?v=sLADei_c9Qg>

## How to use

<video id="myVideo" width="100%" height="auto" controls>
  <source src="./video/bare-metal-kubernetes-hands-on-tutorial-with-maas-and-juju-[sladei_c9qg].mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

The video is divided into several sections 🔖:

- <a href="#" onclick="jumpToTime('00:00')">00:00 Introduction and goals</a>
- <a href="#" onclick="jumpToTime('01:44')">01:44 Setup overview and steps</a>
- <a href="#" onclick="jumpToTime('02:55')">02:55 Installing MAAS, LXD and setting up networking</a>
- <a href="#" onclick="jumpToTime('07:07')">07:07 Configuring MAAS</a>
- <a href="#" onclick="jumpToTime('09:50')">09:50 Creating and tagging machines in LXD using MAAS</a>
- <a href="#" onclick="jumpToTime('16:43')">16:43 Installing juju, bootstrapping the metal cloud, adding machines to Juju</a>
- <a href="#" onclick="jumpToTime('26:20')">26:20 Installing and configuring Ceph storage</a>
- <a href="#" onclick="jumpToTime('30:44')">30:44 Installing K8s cluster and relating it to Ceph</a>
- <a href="#" onclick="jumpToTime('35:42')">35:42 Add K8s cluster to Juju and bootstrap a controller</a>
- <a href="#" onclick="jumpToTime('36:09')">36:09 Deploy hello-kubecon application to the K8s cluster and configure an ingress</a>
- <a href="#" onclick="jumpToTime('38:28')">38:28 Enable external access and test the hello-kubecon application</a>
- <a href="#" onclick="jumpToTime('40:34')">40:34 Scale up and down the K8s cluster and hello-kubecon application using Juju</a>
- <a href="#" onclick="jumpToTime('47:03')">47:03 How to remove things/clean up</a>
- <a href="#" onclick="jumpToTime('49:52')">49:52 Summary and wrapup</a>

<script>
function jumpToTime(time) {
  var video = document.getElementById('myVideo');
  var parts = time.split(':');
  video.currentTime = (+parts[0]) * 60 * 60 + (+parts[1]) * 60;
  video.play();
}
</script>

Read maas-setup.sh. The script is not fully automated and requires manual intervention at times. Read the comments to understand the process.

## Requirements

You need a reasonably powerful **bare metal** machine, 4 or more cores with 32 GB of RAM and 500GB of free disk space. Assumes a fresh install of Ubuntu server (20.04 or higher) on the machine.

You will need to install the command line configuration tool for Kubernetes [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

The reason you need a bare metal machine is because nesting multiple layers of VMs will not work and/or have performance problems.

Note: this tutorial has not been tested on versions prior to 20.04.
