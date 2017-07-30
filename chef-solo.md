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
file_cache_path "/root/.chef/"
cookbook_path "/root/cookbooks"
json_attribs "/root/.chef/runlist.json" 
```
Log level бывают: `:debug, :info, :warn, :error, and :fatal. Default value: :info`

Comunity Cookbooks можно скачать отсюда:
```
https://supermarket.chef.io/cookbooks/
```
Чтобы скачать:
```
git clone https://github.com/miketheman/nginx
```
Чтобы установить зависимости и распаковать кукбук:
```
cd nginx
berks install   (Это если есть Berksfile)
berks package
tar xf tar xf cookbooks-1501414907.tar.gz -C /root/
```
Он будет распакован в папку /root/cookbooks.

`Berksfile` выглядит так:
```
source 'https://supermarket.chef.io'

metadata

group :integration do
  cookbook 'apt', '~> 2.6.1'

  cookbook 'nginx_service_test', path: 'test/fixtures/cookbooks/nginx_service_test'

  cookbook 'yum-epel'

  # Or include an entire directory, once we have more test cookbooks:
  # Dir["test/fixtures/cookbooks/**/metadata.rb"].each do |metadata|
  #   cookbook File.basename(File.dirname(metadata)), path: File.dirname(metadata)
  # end
end
```

Для запуска кукбука на выполнение, необходимо создать файл runlist.json с подобным содержимым:
```
nano /root/.chef/runlist.json
{ 
"run_list": ["recipe[nginx::default]", "recipe[iptables::default]"],
  "nginx": {"default_root":"/usr/share/nginx/html"} 
} 
```

Чтобы запустить кукбук:
```
chef-solo -c /root/.chef/solo.rb
```
