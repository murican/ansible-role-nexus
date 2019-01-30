# ansible-role-nexus
Ansible Role for Sonatype Nexus

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Variables](#variables)
- [Tags](#tags)
- [Usage](#usage)
- [Author](#author)

# Introduction

This Role will install and configure an SonaType Nexus Repository Manager OSS.

https://www.sonatype.com/nexus-repository-oss

Sonatype only provide tar.gz Archives. They provide no official RPM or DEB Packages.
This Role will download & extract the latest archive from sonatype site.

**The inital Admin Login is admin:admin123 and should be changed directly after installation!**

# Requirements

Nexus Requires Java. Java OpenJDK 1.8.0 is defined in the defaults to be installed.

- Ansible minimal Version 2.4


# Variables
| Name | Description | Default |
|:-----|:------------|:--------|
| nexus_service_names | List of service names | nexus |
| nexus_service_state | Service state | started |
| nexus_service_enabled | Service enabled | true |
| nexus_download_url | URL to fetch the archive from | Origin SonaType Download URL |
| nexus_tmp_archive_file | Path to Downloaded Temp File | /tmp/nexus.tar.gz |
| nexus_java_package_name  | Name of the Java Package to install | java-1.8.0-openjdk |
| nexus_java_package_state | State of the Java Package | present
| nexus_user_name  | Name of the System User for Nexus | nexus |
| nexus_group_name | Name of the System Group for Nexus | nexus |
| nexus_user_id | Optional: UID for the User | not set(omit) |
| nexus_group_id | Optional: GID for the Group | not set(omit) |
| nexus_base_path | Path where the Software is installed and Data are stored | /var/lib/nexus |
| nexus_log_path | Log Directory Path | {{ nexus_base_path }}/data/log |
| nexus_data_path | Relative Path to Data Folder from base | ../data |
| nexus_tmp_path | Relative Path to Tmp Folder | ../data/tmp |
| nexus_max_memory_size | Max Memory Size for JVM Process | 2G |
| nexus_limit_nofile | Security Limits Nofile Value | 65536 |
| nexus_java_heap_mem_xms | Initial Memory for JVM -Xms | 256M |
| nexus_java_heap_mem_xmx | Max Memory for JVM -Xmx | 1500M |


# Tags
- nexus: run all tasks from this role
- nexus-user: setup system user __nexus_user_name__ and system group __nexus_group_name__
- nexus-download: download the archive from the official sonatype site.
- nexus-dir: ensure needed __nexus_base_path__ and __nexus_sub_directories__ ; ensures owner and permissions
- nexus-install: ensure that package __nexus_java_package_name__ are in state __nexus_java_package_state__ ; extract the downloaded archive and set owner.
- nexus-config: ensure configuration of vmoptions and limits file
- nexus-service: ensure that all services in __nexus_service_names__ are in state __nexus_service_state__

# Usage

Example playbook

```yaml
- hosts: 127.0.0.1
  roles:
  - role: nexus
```

# Author
Jens Schneider
