# memcached installations and usage

### Installation on mac and redhat\/centos

* On mac

  ```shell
  $ brew install memcached
  $ memcached -p 11211
  ```

* On linux as root

  ```shell
  $ yum install memcached
  $ /etc/init.d/memcached start/stop/status

  Config file location
  $ cat /etc/sysconfig/memcached
  ```


