
# luci-app-zerotier

LuCI for ZeroTier / ZeroTier 的 LuCI 管理界面

- 用于加入 ZeroTier 网络的 LuCI 管理界面
- 使用脚本动态实现 NAT 功能（多子网互连），更具灵活、方便
- 适用于 OpenWrt 官方和 [LEDE](https://github.com/coolsnowwolf/lede)

本项目从 <https://github.com/coolsnowwolf/luci> 拷贝过来


## Depends / 依赖

- zerotier
- luci-compat (For OpenWrt 官方 luci)

## Compile / 编译

```shell
# 安装依赖
sudo apt update -y && sudo apt full-upgrade -y

sudo apt install -y \
ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libfuse-dev libglib2.0-dev libgmp3-dev \
libltdl-dev libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libpython3-dev libreadline-dev \
libssl-dev libtool lrzsz mkisofs msmtp ninja-build p7zip p7zip-full patch pkgconf python3 \
python3-pyelftools python3-setuptools qemu-utils rsync scons squashfs-tools subversion swig texinfo \
uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev bc lm-sensors pciutils libpam0g-dev libkmod-dev \
liblzma-dev libpcre2-dev libsnmp-dev libcurl4-openssl-dev libtins-dev libyaml-cpp-dev libgpiod-dev \
libtirpc-dev libaio-dev


# 进入 OpenWrt SDK 目录，建议使用 Docker，如:
docker run -it -v $PWD/bin:/builder/bin openwrt/sdk:x86-64-22.03.5 bash

# 要更新 feeds
#   - 获取 feeds/luci/luci.mk
#   - 获取依赖包 zerotier 编译信息 (feeds/packages/net)
#   - 获取 feeds/luci/applications 目录
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig


# 拷贝到合适目录，如
git clone --depth=1 https://github.com/mmc1987/luci-app-zerotier.git feeds/luci/applications/luci-app-zerotier

# 加载
./scripts/feeds update -f luci
./scripts/feeds install -p luci -f luci-app-zerotier
make defconfig

# 编译
make package/luci-app-zerotier/compile

make download -j8
make V=s -j1


# 结果
# 存放在 bin/packages/x86_64/luci 目录
luci-app-zerotier*.ipk
luci-i18n-zerotier-zh-cn*.ipk
```
