# 自定义类型

![image.png](https://upload-images.jianshu.io/upload_images/14466577-6a4e69e895734439.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### JavaBean

```
@Override
	public void write(DataOutput paramDataOutput) throws IOException {
		// TODO Auto-generated method stub
		
		paramDataOutput.writeInt(this.uploadStream);
		paramDataOutput.writeInt(this.downloadStream);
		paramDataOutput.writeInt(this.sumStream);

	}
	@Override
	public void readFields(DataInput paramDataInput) throws IOException {
		// TODO Auto-generated method stub
		
		uploadStream = paramDataInput.readInt();
		downloadStream = paramDataInput.readInt();
		sumStream = paramDataInput.readInt();
		
	}
	@Override
	public int compareTo(Object paramT) {
		// TODO Auto-generated method stub
		SortBean beanOne = (SortBean)paramT;
		System.out.println("this:"+this);
		System.out.println("beanone:"+beanOne);
		return this.sumStream>beanOne.sumStream?1:-1;
	}
```
	自定义类型作为value，只使用Writable接口就可以；
	* 自定义类型作为key,首先还需要序列化，同时key是要排序的，
	我们必须提供compareTo方法，需要实现Comparable接口，故使
	用Writable和Comparable最方便.
	* 如果不设置compareTo():
 
![image.png](https://upload-images.jianshu.io/upload_images/14466577-21440808d779ea7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### driver区
 
```
package com.lanou.test;

import java.io.IOException;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import com.lanou.model.SortBean;
import com.lanou.util.SortMapper;
import com.lanou.util.SortReduce;

public class SortTest {
	
	public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
		//总流量 上行流量 下行流量 ，手机号
		//key              value
		//总流量进行排序
		//把上次计算后的内容作为这次计算的输入
		//多MapReduce串行
		
		/*
	 * 从log中获取手机号 上行下行流量 总流量
	 * reduce之后 手机号 流量对象
	 *
	 *使用自定义类型输出
	 *1.要根据我们的数据进行建模(创建实体类)
	 *2.mapper形参怎么写 map()方法当中怎么对数据进行切割筛选
	 *将我们的数据放入bean中 想好将bean以key,还是value进行输出
	 *3.map的结果最终要写入磁盘,所以自定义bean要支持序列化
	 *Serializble是Java提供重量级序列化 在我们hadoop更建
	 *使用hadoop自身提供的WritableComparable来实现序列化和反序列化
	 *这时有write()写入文件和readFields()从文件中读取的方法实现
	 *否则在reduce阶段是获取不到数据的 而这里一定要注意的一点是readFields()方法
	 *调用read()的时候要按照写入的顺序获取
	 *4.reduce当中注意形参和输出位置,以及driver 区对应好输出类型
	 *
	 *job.setOutputKeyClass(Text.class);
	 *job.setOutputValueClass(StreamBean.class);
	 *
	 *5.一切OK后,reduce就可以正常输出到我们指定的位置
	 *但注意bean的toString()方法要重写
	 */
		
		//这里driver简写
		Configuration conf = new Configuration();
		Job job = Job.getInstance(conf,"sort bean");
		job.setJarByClass(SortTest.class);
		job.setMapperClass(SortMapper.class);
		job.setCombinerClass(SortReduce.class);
		job.setReducerClass(SortReduce.class);
		job.setOutputKeyClass(SortBean.class);
		job.setMapOutputValueClass(Text.class);
		
		FileInputFormat.addInputPath(job, new Path("D:\\hadoop-2.7.3\\mapreduce\\output\\beanoutput\\part-r-00000"));
		FileOutputFormat.setOutputPath(job, new Path("D:\\hadoop-2.7.3\\mapreduce\\output\\sortoutput1"));
		boolean waitForCompletion = job.waitForCompletion(true);
		System.exit(waitForCompletion?0:1);
	}
}
```

### mapper区

```
public class SortMapper extends Mapper<Object, Text, SortBean, Text> {
	private Text phoneText = new Text();
	@Override
	protected void map(Object key, Text value, Mapper<Object, Text, SortBean, Text>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		String[] vals = value.toString().split("\\s+");
		String phone = vals[0];
		String uploadStream = vals[1];
		String downloadStream = vals[2];
		String sumStream = vals[3];
		//将截取的数据存入bean实例中
		SortBean sortBean = new SortBean(uploadStream,downloadStream,sumStream);
		phoneText.set(phone);
		context.write(sortBean, phoneText);
	}
}
```

### reducer区

```
@Override
	protected void reduce(SortBean key, Iterable<Text> value, Reducer<SortBean, Text, SortBean, Text>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		//value只有一个数据所以直接获取不用foreach
		context.write(key, value.iterator().next());
	}
```