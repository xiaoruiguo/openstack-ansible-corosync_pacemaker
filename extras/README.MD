将 corosync-pacemaker-install.yml 拷贝到openstack-ansible的 playbook目录中将本角色拷贝到 playboo/roles 目录中。
个别模块支持ansible的版本<2.3，如果大于此版本，则需要修改。再部署是需要先执行 haproxy-install.yml ，部署完成后才能正确执行本角色。
/etc/openstack_deploy/user_variables中，需要禁止keepalived的使用。
将本yml文件放在 setup-infrastructure.yml中haproxy-install.yml的后面。可以连续执行。

openstack-ansible corosync-pacemaker-install.yml


#/etc/openstack_deploy/user_variables.yml
haproxy_use_keepalived: False


#setup-infrastructure.yml
---
# Copyright 2014, Rackspace US, Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

- include: unbound-install.yml
- include: repo-install.yml
- include: haproxy-install.yml
- include: corosync-pacemaker-install.yml
- include: memcached-install.yml
- include: galera-install.yml
- include: rabbitmq-install.yml
- include: etcd-install.yml
- include: ceph-install.yml
- include: utility-install.yml
- include: rsyslog-install.yml