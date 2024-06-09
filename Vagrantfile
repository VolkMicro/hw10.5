Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  
  config.vm.provision "shell", inline: <<-SHELL
    # Обновление пакетов и установка зависимостей
    sudo apt-get update
    sudo apt-get install -y wget build-essential libreadline-dev zlib1g-dev flex bison
    
    # Скачивание исходного кода PostgreSQL 8.4.22 через HTTP
    wget https://ftp.postgresql.org/pub/source/v8.4.22/postgresql-8.4.22.tar.gz
    
    # Распаковка исходного кода
    gunzip postgresql-8.4.22.tar.gz
    tar xf postgresql-8.4.22.tar
    
    # Сборка и установка PostgreSQL
    cd postgresql-8.4.22
    ./configure
    make
    sudo make install
    
    # Создание необходимых директорий
    sudo mkdir /usr/local/pgsql/data
    sudo chown vagrant /usr/local/pgsql/data
    
    # Инициализация базы данных
    /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
    
    # Запуск сервера PostgreSQL
    /usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
    
    # Добавление пути к исполняемым файлам PostgreSQL в PATH
    echo 'export PATH=$PATH:/usr/local/pgsql/bin' >> /home/vagrant/.bashrc
  SHELL
end

