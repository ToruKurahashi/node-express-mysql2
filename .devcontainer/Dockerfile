FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    ca-certificates

# Node.js LTS（公式NodeSource）を追加してインストール
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - \
    && apt-get install -y nodejs

# MySQLインストール
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server && \
    rm -rf /var/lib/apt/lists/*

# MySQLが起動する状態でコンテナに入るための設定
RUN mkdir -p /var/run/mysqld && \
    chown -R mysql:mysql /var/run/mysqld

# MySQL起動→rootの認証方式変更→パスワード設定
RUN service mysql start && \
    mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'; FLUSH PRIVILEGES;"
