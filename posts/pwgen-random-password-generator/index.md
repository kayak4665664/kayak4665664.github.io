# Pwgen: a Random Password Generator

pwgen can generate random and secure passwords in the command line!
&lt;!--more--&gt;

{{&lt; link href=&#34;https://pwgen.sourceforge.io/&#34; title=&#34;pwgen&#34; content=&#34;pwgen&#34; card=true &gt;}}

pwgen can be installed with Homebrew: `brew install pwgen`.

The usage is also very simple. For example, `pwgen -sy 50` is to generate a 50-character password, including uppercase and lowercase letters, numbers and special characters. More usage can be viewed with `pwgen -h`:

{{&lt; admonition note &gt;}}
Usage: pwgen [ OPTIONS ] [ pw_length ] [ num_pw ]  

Options supported by pwgen:  
  -c or --capitalize  
	Include at least one capital letter in the password  
  -A or --no-capitalize  
	Don&#39;t include capital letters in the password  
  -n or --numerals  
	Include at least one number in the password  
  -0 or --no-numerals  
	Don&#39;t include numbers in the password  
  -y or --symbols  
	Include at least one special symbol in the password  
  -r &lt;chars&gt; or --remove-chars=&lt;chars&gt;  
	Remove characters from the set of characters to generate passwords  
  -s or --secure  
	Generate completely random passwords  
  -B or --ambiguous  
	Don&#39;t include ambiguous characters in the password  
  -h or --help  
	Print a help message  
  -H or --sha1=path/to/file[#seed]  
	Use sha1 hash of given file as a (not so) random generator  
  -C  
	Print the generated passwords in columns  
  -1  
	Don&#39;t print the generated passwords in columns  
  -v or --no-vowels  
	Do not use any vowels so as to avoid accidental nasty words  
{{&lt; /admonition &gt;}}

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/pwgen-random-password-generator/  

