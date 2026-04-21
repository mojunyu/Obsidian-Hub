## PHP版本

1. 先添加系统环境变量

2. 创建两个批处理文件，比如 `php74.bat` 和 `php82.bat`。

3. 在 `php74.bat` 中，输入以下内容：

   ```bat
   @echo off
   D:\phpEnv\php\php-7.4\php.exe %*
   ```

   在 `php82.bat` 中，输入以下内容：

   ```bat
   @echo off
   D:\phpEnv\php\php-8.2\php.exe %*
   ```

4. 将这两个批处理文件放入某个已在 `PATH` 中的目录中（如 `C:\Windows\System32`），这样你就可以在命令行中直接输入 `php74` 或 `php82` 来切换版本。

5. 命令行输入 php82 或者 php74 来切换



## composer版本

1. **创建 `composer.bat` 文件**：

2. 为每个 PHP 版本创建一个批处理文件来调用 `composer`，例如 `composer74.bat` 和 `composer82.bat`。

   创建 `composer74.bat`：

   ```bat
   @echo off
   D:\phpEnv\php\php-7.4\php.exe D:\phpEnv\tools\Composer\composer.phar %*
   ```

   创建 `composer82.bat`：

   ```bat
   @echo off
   D:\phpEnv\php\php-8.2\php.exe D:\phpEnv\tools\Composer\composer.phar %*
   ```

3. **将 `composer.bat` 文件所在的路径加入系统环境变量 `PATH`**：确保你创建的 `.bat` 文件所在目录被添加到系统的 `PATH` 环境变量中，以便你可以从任何地方调用这些命令。

