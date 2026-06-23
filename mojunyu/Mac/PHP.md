

```bash

brew search php@
brew install php@8.1

这是一个方便的小工具，可以快速切换 PHP 版本，并自动更新你的 PATH 和相关配置。

brew install brew-php-switcher

brew-php-switcher 7.4
brew-php-switcher 8.1


# 切换版本后，fpm
brew services stop php@8.1
brew services start php@7.4
ps aux | grep php-fpm

```