# awk


awk -F 'updateCycle' 'NR==1 {printf $1 "resourceUpdateType\":\"02\",\"updateCycle" $2}' /tmp/dd
