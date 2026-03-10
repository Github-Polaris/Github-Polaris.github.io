添加submodule
git submodule add https://github.com/Github-Polaris/hugo-theme-stack/ themes/hugo-theme-stack

删除submodule
vim .gitmodules并删除你想要移除的submodule配置
vim .git/config并删除你想要移除的submodule配置
git rm --cached path/to/submodule
rm -rf .git/modules/path/to/submodule
rm -rf path/to/submodule
