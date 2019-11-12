# awk

awk '{pattern + action}' {filenames}

内置变量，argc：命令行参数个数；argv：命令行参数列表；environ：支持队列中系统环境变量的使用；filename：文件名；fnr：文件记录数；fs：设置输入域分隔符，等价于-F；nf：记录域的个数，列数；nr：已读记录数；ofs：输出域分割符；ors：输出记录分隔符；rs：控制记录分隔符；$0，整体记录；$1，第一列；$nf，最后一列；



awk -F 'updateCycle' 'NR==1 {printf $1 "resourceUpdateType\":\"02\",\"updateCycle" $2}' /tmp/dd

awk -F "[/]" 'NR == 4 {print $0,"\n",$1}' /etc/passwd

awk -F ":"  '{if(NR<31 && NR >12) print $1}' /etc/passwd 

last | awk '{S[$3]++} END{for(a in S ) {print S[a],a}}' |uniq| sort -rh 

awk -F ':' 'BEGIN {count=0;} {name[count] = $1;count++;}; END{for (i = 0; i < NR; i++) print i, name[i]}' /etc/passwd
