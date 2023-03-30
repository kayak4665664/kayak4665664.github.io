# pwgen: 随机密码生成器

pwgen可以在命令行中生成随机又安全密码！
<!--more-->

{{< link href="https://pwgen.sourceforge.io/" title="pwgen" content="pwgen" card=true >}}

直接使用Homebrew安装：`brew install pwgen`。

用法也很简单，比如`pwgen -sy 50`就是生成50个字符的密码，包含大小写字母、数字和特殊字符。更多用法可以使用`pwgen -h`查看：

{{< admonition note >}}
Usage: pwgen [ OPTIONS ] [ pw_length ] [ num_pw ]  

Options supported by pwgen:  
  -c or --capitalize  
	Include at least one capital letter in the password  
  -A or --no-capitalize  
	Don't include capital letters in the password  
  -n or --numerals  
	Include at least one number in the password  
  -0 or --no-numerals  
	Don't include numbers in the password  
  -y or --symbols  
	Include at least one special symbol in the password  
  -r <chars> or --remove-chars=<chars>  
	Remove characters from the set of characters to generate passwords  
  -s or --secure  
	Generate completely random passwords  
  -B or --ambiguous  
	Don't include ambiguous characters in the password  
  -h or --help  
	Print a help message  
  -H or --sha1=path/to/file[#seed]  
	Use sha1 hash of given file as a (not so) random generator  
  -C  
	Print the generated passwords in columns  
  -1  
	Don't print the generated passwords in columns  
  -v or --no-vowels  
	Do not use any vowels so as to avoid accidental nasty words  
{{< /admonition >}}

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/pwgen-random-password-generator/  

