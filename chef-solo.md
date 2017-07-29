### Chef-solo
Используется для применения конфигурации на конкретном хосте, там где он установлен.

Чтобы установить chef-solo, необходимо выполнить следующие команды:
```
wget https://packages.chef.io/files/stable/chef/13.2.20/el/7/chef-13.2.20-1.el7.x86_64.rpm
rpm -ivh chef-13.2.20-1.el7.x86_64.rpm
wget https://packages.chef.io/files/stable/chefdk/2.0.28/el/7/chefdk-2.0.28-1.el7.x86_64.rpm
rpm -ivh chefdk-2.0.28-1.el7.x86_64.rpm
```

Для конфигурации надо создать файл:
```
mkdir ~/.chef/
touch ~/.chef/solo.rb
```
И внести в него настройки:
```
log_level :debug
file_cache_path "~/.chef/"
cookbook_path "~/chef_cookbooks"
json_attribs "~/.chef/runlist.json"
```
Log level бывают: `:debug, :info, :warn, :error, and :fatal. Default value: :info`
