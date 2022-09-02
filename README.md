### eslint && prettier && Git hooks

#### prettier 设置

1、npm i prettier --save-dev
2、echo {}> .prettierrc.json
3、在线格式化规则设置
https://www.prettier.cn/playground/#N4Igxg9gdgLgprEAuEAzArlMMCW0AEAEnADYkQDqEATiQCYAUwA5tXHLlM-gLz4A6IABalyggDT5W7eHV74A5IKq06ghZIDOOEghjzUAQxKa4k6AFkI6UwHkAbnGriAvgEp8wflG-58OVAYAQmkOHC43YDYYdGoofCh0MhcAbm9fPz8Aeiz8ABVbABFbJHxC6AV9Gzh8akMoOggAW394tganDN19RJa+C0MYIQA6VHIafAYBoeG6huaGDwAqfABGAFEAagB2N2GYCABlGGpw5kXZuAAHEkMwOAYs-n5h57pNrJxmSUFBN3T4rUOLF4gAeOg4ez4MC3TSaAByhiacB4CmIZEoNHoCnwuBguh4wAABgBNaz4QxsfD2HDaA7UBLoJoAIyc+AAJMBGS0XESXPhLNY7I5qITBdUHE4XAA+AGZfCgzQnaDMaVc0KcZjDTQkHD3Bj4AAMklW+D2BwAqlcrk4AMKGUyLfCbKRsMJcbW6-Wrc0QAAyEAA7naHQ8PC5QVkldQVbLAX4WG7NcMEHRNBQcEMGBI-vgAPwCECF-ClRVXer4JUATwJwGAkHI1FKSn40irChcMokhcjmnLUGl+BcGT8oLgTTj-Bg6qTcDkw58MEj47j8q5DG0ulg-3jmQLgleIBHmVKgiCggXx8jEPs0rSPigLhA4hAECuuGgmmQoEpMcDAAVKQQL8UGMQNDCrL8X2ZOowAAaw4Q4kTgP1wjgZAjBMMwQBgu4EJgQ5yzAM5kBOdBsPHVk6DoOc-XqZh0EMZg4AAMRoJpBk1ZAQEMdADmfYQYCaEgKCETM4D7O44EOYDM0hTMq24sA4QE8JTGoGB-zqZgOIw4xTBfAArTQAA9DjOXQAEV0AgeA9Kwl9y2odTuOZQxWRIASrlOWAMzoIZkAADmNEBvIgUwKDqK5uO8iSnEcASAEcbPgLS3xAnjNAAWigdgaLoAS2GSnA2C0pjdKQTCDJAUwmhwUjqHIl9tC4KyUvQpAyOwmB3L8gKkAAJhfE5DB0M5bWaCqQAkgBWATqjydyQKq7D7HIgBJDpYEOMBTnfABBBpjhrDqVs7IA
4、新建.prettierignore，配置忽略格式化的文件
5、npx prettier --write src/ 指定的文件夹代码格式化

### eslint 安装

1、npm i eslint --save
2、初始化配置文件 ./node_modules/.bin/eslint --init
3、配置文件 extends 新增 extends: [...arr, prettier] 放在最后，可以覆盖 eslint 部分配置
4、可以安装 eslint-config-prettier，关闭某些和 prettier 不太兼容的规则
https://github.com/prettier/eslint-config-prettier#installation

### Git hooks

1、npm install --save-dev husky lint-staged
2、npx husky install
3、npm set-script prepare "husky install"
4、npx husky add .husky/pre-commit "npx lint-staged"

#### 编辑器设置

1、安裝插件 Prettier - Code formatter
2、Vscode -》 首选项 -》 设置（搜索 save）-》 勾选 Editor: Format On Save 即可
