# 使用官方 PostgreSQL 17 镜像作为基础 (*** 已更新 ***)
FROM postgres:17

# 安装编译 pg_mq 所需的依赖
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    postgresql-server-dev-17 \
    && rm -rf /var/lib/apt/lists/*

# 克隆、编译并安装 pgmq
# 注意：请确保您使用的 pgmq 版本与 PostgreSQL 17 兼容。v1.2.0 是一个示例。
RUN git clone --branch v1.2.0 https://github.com/tembo-io/pgmq.git /pgmq \
    && cd /pgmq/pgmq-extension \
    && make \
    && make install \
    && install-pg-partman

# 将初始化脚本复制到容器中
COPY init.sql /docker-entrypoint-initdb.d/
