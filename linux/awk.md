# awk

awk '{pattern + action}' {filenames}

内置变量，argc：命令行参数个数；argv：命令行参数列表；environ：支持队列中系统环境变量的使用；filename：文件名；fnr：文件记录数；fs：设置输入域分隔符，等价于-F；nf：记录域的个数，列数；nr：已读记录数；ofs：输出域分割符；ors：输出记录分隔符；rs：控制记录分隔符；$0，整体记录；$1，第一列；$nf，最后一列；

交集
awk 'NR==FNR{ a[$1]=a[$1]+1} NR>FNR{ if(a[$1]>=1 &&b[$1]<1){ print $1;b[$1]=b[$1]+1}}' aaa.txt bbb.txt 
awk 'NR==FNR && NF {a[$1]+=1;} NR>FNR && NF {if(a[$1]>=1 && b[$1]<1){print $1;b[$1]+=1 }}' a.sf b.sf
差集
awk 'NR==FNR{ a[$1]=$1 } NR>FNR{ if(a[$1] == ""){ print $1}}' aaa.txt bbb.txt

awk -F 'updateCycle' 'NR==1 {printf $1 "resourceUpdateType\":\"02\",\"updateCycle" $2}' /tmp/dd

awk -F "[/]" 'NR == 4 {print $0,"\n",$1}' /etc/passwd

awk -F ":"  '{if(NR<31 && NR >12) print $1}' /etc/passwd 

last | awk '{S[$3]++} END{for(a in S ) {print S[a],a}}' |uniq| sort -rh 

awk -F ':' 'BEGIN {count=0;} {name[count] = $1;count++;}; END{for (i = 0; i < NR; i++) print i, name[i]}' /etc/passwd

awk 'gsub(/\047|\,/,"") {print "/**", $4,"*/", "\n","private String", $1;}' tt.txt 
上面gsub模式匹配失败会导致后面的不执行，从而没有任何输出；下面这样写则没有该问题；另外对于win下面的^M字符，可以在vim中通过:s/^M//g删除，^M的输入方法为：C-v,C-m；
awk '{gsub(/\047|\,/,""); print "/**", $4,"*/", "\n","private String", $1;}' tt.txt 


# sed 

sed '1~2d' 1.txt   #从第一行开始删除，每隔2行就删掉一行，即删除奇数行

sed  '/123/,$d'  1.txt  #删除从匹配123的行到最后一行

sed  '/123/,+1d'  1.txt   #删除匹配123的行及其后面一行`

sed  '/^$/d'    1.txt    #删除空行

sed  '1,3{/123/d}'   1.txt     #删除1~3行中，匹配内容123的行，1,3表示匹配1~3行，{/123/d}表示删除匹配123的行

sed  's/123/hello/g'  1.txt #将文本中所有的123都替换为hello

sed 's/123/hello/2'   1.txt  #将每行中第二个匹配的123替换为hello

sed  -n 's/123/hello/gpw  2.txt'   1.txt    #将每行中所有匹配的123替换为hello，并将替换后的内容写入2.txt

sed  's/..$//g'  1.txt  #替换每行中的最后两个字符为空，每个点代表一个字符，$表示匹配末尾  （..$）表示匹配最后两个字符

sed 's/^#.*//;/^$/d'  1.txt  #先替换1.txt文件中所有注释的空行为空行，然后删除空行，替换和删除操作中间用分号隔开

sed 's/^[0-9]/(&)/'   1.txt   #将每一行中行首的数字加上一个小括号   (^[0-9])表示行首是数字，&符号代表匹配的内容;或者：sed 's/[0−9]/(\1)/'   1.txt  #替换左侧特殊字符需钥转义，右侧不需要转义，\1代表匹配的内容



