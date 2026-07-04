
## way 1. 找一个类似的扫地机型号接入进来

# 从 Home Assistant 控制台登录，获得 shell 环境后执行以下命令

# Step 1: 获取正在运行的 Docker 容器 ID，其中包含 Home Assistant 的实例
docker ps | grep homeassistant
# `docker ps` 列出所有正在运行的容器，`grep` 筛选出名字中包含 "homeassistant" 的容器。

# Step 2: 使用容器 ID 进入 Home Assistant 容器内部
docker exec -it <CONTAINERID> sh
# 替换 <CONTAINERID> 为上一步中返回的容器 ID。
# `-it` 以交互模式进入容器，`sh` 打开一个 Shell 环境。

# Step 3: 定位到 deebot_client 的 hardware/deebot 目录
cd /usr/local/lib/python3.13/site-packages/deebot_client/hardware/deebot
# 这里的路径是 Python 的 site-packages 目录，存放 Python 库文件。
# deebot_client 是与扫地机器人（如 Ecovacs Deebot）交互的模块。

# Step 4: 创建一个符号链接，将 x5d34r.py 文件指向 lhbd50.py
ln -svfT x5d34r.py lhbd50.py
# `ln` 是创建链接的命令。
# `-s` 创建符号链接，类似于快捷方式。
# `-v` 显示创建链接的详细信息。
# `-f` 强制覆盖已存在的目标文件。
# `-T` 明确目标是文件（而非目录）。
# 这一步确保任何对 lhbd50.py 的引用都指向 x5d34r.py。

# Step 5: 重启 Home Assistant 以使更改生效
restart home assistant
# 通过重启让新的符号链接及代码修改生效

## way 2. 自写集成，用Offical Ecovacs mcp server接入Home Assistant

举例：https://github.com/mslycn/ecovacs_cn

## way 3. 自写集成，用Offical Ecovacs skill server api接入Home Assistant
