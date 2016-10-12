---
layout: post
title:  "Vagrant en Fedora 24"
date:   2013-06-05 17:06:25
categories: Fedora Vagrant
---

Esta última semana estuve leyendo [Ansible][Ansible] y [Vagrant][Vagrant] y me encontré con que el paquete de vagrant-libvirt que esta en los repos de Fedora da
problemas con Nekogiri, que es una gema de ruby.


{% highlight bash %}
# Descargamos la llave, suma y rpm
wget https://keybase.io/hashicorp/key.asc -O hashicorp.asc &
wget https://releases.hashicorp.com/vagrant/1.8.6/vagrant_1.8.6_SHA256SUMS.sig &
wget https://releases.hashicorp.com/vagrant/1.8.6/vagrant_1.8.6_SHA256SUMS &
wget https://releases.hashicorp.com/vagrant/1.8.6/vagrant_1.8.6_x86_64.rpm
# Verificamos la suma
gpg --import hashicorp.asc
gpg --verify vagrant_1.8.6_SHA256SUMS.sig vagrant_1.8.6_SHA256SUMS
sha256sum -c vagrant_1.8.6_SHA256SUMS
# Instalamos
sudo rpm -ivh vagrant_1.8.6_x86_64.rpm
# Instalamos las dependencias del plugin
dnf -y install qemu libvirt libvirt-devel ruby-devel gcc
# Instalamos el plugin para usar libvirtd como provider
vagrant plugin install vagrant-libvirt
{% endhighlight %}

Y listo! :D


[Ansible]: https://www.ansible.com/
[Vagrant]: https://www.vagrantup.com/
