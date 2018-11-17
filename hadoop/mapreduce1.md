# MapReduce

## 第一步还是引入jar包(步骤如hdfs篇)

##### MapReduce 适合离线处理，不擅长实时计算，流式计算
##### 并行编程模型：用于对大规模数据集（大于1TB）的并行处理

### MapReduce()只需要制定两个方法：
##### map()：对元素进行制定操作，可以高度并行
##### reduce（）：对列表元素进行合并

## WordCount实例

![image.png](https://upload-images.jianshu.io/upload_images/14466577-a4907da159050d4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
package com.lanou.test;

import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

import com.lanou.util.CountMapper;
import com.lanou.util.CountReduce;

public class WordCountTest {

	//mapper区
	 public static class TokenizerMapper
	    extends Mapper<Object, Text, Text, IntWritable>
	  {
	    private static final IntWritable one = new IntWritable(1);
	    private Text word = new Text();
	    //key默认是字节偏移量,value是获取的一行内容
	    public void map(Object key, Text value, Mapper<Object, Text, Text, IntWritable>.Context context)
	      throws IOException, InterruptedException
	    {
			//分割每个单词计数1
	      StringTokenizer itr = new StringTokenizer(value.toString());
	      while (itr.hasMoreTokens())
	      {
	        this.word.set(itr.nextToken());
	        //如果我们使用自定义类需要序列化 因为会写入文件
	        //将处理的数据以需要的形式进行写入
	        context.write(this.word, one);
	      }
	    }
	  }
	  
	  //reducer区
	  public static class IntSumReducer
	    extends Reducer<Text, IntWritable, Text, IntWritable>
	  {
	    private IntWritable result = new IntWritable();
	    //
	    public void reduce(Text key, Iterable<IntWritable> values, Reducer<Text, IntWritable, Text, IntWritable>.Context context)
	      throws IOException, InterruptedException
	    {
	      int sum = 0;
	      for (IntWritable val : values) {
	        sum += val.get();
	      }
	      this.result.set(sum);
	      context.write(key, this.result);
	    }
	  }
	  
	  //driver区
	  public static void main(String[] args)
	    throws Exception
	  {
	    Configuration conf = new Configuration();
	    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
	    if (otherArgs.length < 2)
	    {
	      System.err.println("Usage: wordcount <in> [<in>...] <out>");
	      System.exit(2);
	    }
	    //工作
	    Job job = Job.getInstance(conf, "word count");
	    //打包
	    job.setJarByClass(WordCountTest.class);
	    //设置map
	    job.setMapperClass(CountMapper.class);
	    //合并
	    job.setCombinerClass(IntSumReducer.class);
	    //设置reduce
	    job.setReducerClass(CountReduce.class);
	    
	    //设置输出结果类型
	    job.setOutputKeyClass(Text.class);
	    job.setOutputValueClass(IntWritable.class);
	    for (int i = 0; i < otherArgs.length - 1; i++) {
	    	//告诉job我们要读取的路径(除了输出路径的其他参数)
	      FileInputFormat.addInputPath(job, new Path(otherArgs[i]));
	    }
	    //设置输出路径文件夹(最后一个参数)
	    FileOutputFormat.setOutputPath(job, new Path(otherArgs[(otherArgs.length - 1)]));
	    //将我们是设置好的job真正提交给yarn帮我们分配资源,开始工作根据返回值判断是否退出
	    System.exit(job.waitForCompletion(true) ? 0 : 1);
	  }
}
```
 