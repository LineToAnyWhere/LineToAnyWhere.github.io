* 递归输出文件权限，所属用户组，所属用户，绝对路径  
> find $pwd | xargs ls -ld | sed 's/  */ /g' | cut -d ' ' -f 1,3,4,9
* 不递归输出文件权限，所属用户组，所属用户，绝对路径
> find $PWD -maxdepth 1 | xargs ls -ld
* 使用正则输出文件权限，所属用户组，所属用户，绝对路径
> ll $pwd | sed "s: [0-9]*\:[0-9]* : \`pwd\`\/:g" | sed "s/  */ /g" | cut -d ' ' -f 1,3,4,8 | sed '1d'


账户的所属组信息
groups `cat /etc/passwd | cut -d ':' -f 1` | cut -d ':' -f 2 | sed 's/ //' | sed 's/ /|/g' > b.out
账户信息
cat /etc/passwd | cut -d ':' -f 1,2,3,4,6,7 | sed 's/:/ /g' > a.out
合并文件
paste a.out b.out
