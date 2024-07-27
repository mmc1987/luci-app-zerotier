# luci-app-zerotier

Compile / 编译

# 进入 OpenWrt SDK 目录，建议使用 Docker，如:
docker run -it -v $PWD/bin:/builder/bin openwrt/sdk:x86-64-22.03.5 bash

# 要更新 feeds
#   - 获取 feeds/luci/luci.mk
#   - 获取依赖包 zerotier 编译信息 (feeds/packages/net)
#   - 获取 feeds/luci/applications 目录
./scripts/feeds update -a

# 拷贝到合适目录，如
git clone --depth=1 https://github.com/zhengmz/luci-app-zerotier.git feeds/luci/applications/luci-app-zerotier

# 加载
./scripts/feeds update -f luci
./scripts/feeds install -p luci -f luci-app-zerotier
make defconfig

# 编译
make package/luci-app-zerotier/compile

# 结果
# 存放在 bin/packages/x86_64/luci 目录
luci-app-zerotier*.ipk
luci-i18n-zerotier-zh-cn*.ipk
