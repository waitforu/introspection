## 切换国内镜像
`composer config -g repo.packagist composer https://packagist.phpcomposer.com`
## 新功能
- 从本地 git 仓库检出 commit 时提升了安装和更新的效率
- 新增 `check-platform-reqs` 命令，用于检查本地安装的 PHP 和扩展模块的版本是否满足安装包的需求
- 新增了对 SPDX 协议标识 v3.0 的支持，并且不再建议使用 GPL/LGPL/AGPL 标识，这样就可以添加 -only 或 -or-later 后缀了
- 新增了对 --with-all-dependencies 参数的支持，用于 update 和 require 命令执行时更新所有列出的依赖包
- 新增了在 composer.json 文件中对 scripts-descriptions 键的支持，用于自定义描述并对自定义命令添加文档说明
- 新增对全大写的 NO_PROXY 环境变量的支持
- 新增了对 COMPOSER_DEFAULT_{AUTHOR,LICENSE,EMAIL,VENDOR} 环境变量的支持，用于预先填充 init 命令
- 新增了对 COMPOSER_MEMORY_LIMIT 环境变量的支持，以便让 Composer 明确设置 PHP 内存的限制值
- 对于可执行文件增加了简单字符串（simple strings）的支持
- 新增对本地很古老的代码仓库的支持
- 新增了对执行 init 和 require 命令时对输入的 package 名称提供拼写建议的功能
- 修复了对 installed.json 文件中的数据按照 package 名称以字母顺序排序的问题
- 修复了与 Symfony 4.x 组件的兼容，此组件是 Composer 所使用的
