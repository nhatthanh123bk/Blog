### Các kỹ năng khi làm việc trên Linux
HDFS_PATH=/nhatthanh/data/ml-20m/ratings.csv
if hdfs dfs -test -f $HDFS_PATH; then
    echo "[$HDFS_PATH] exists on HDFS"
    hdfs dfs -ls $HDFS_PATH
fi