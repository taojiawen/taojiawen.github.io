# Mapreduce 分区

# driver区

如果reduceTask的数量>= getPartition的结果数  ，则会多产生几个空的输出文件part-r-000xx
如果 1 < reduceTask的数量 < getPartition的结果数 ，则有一部分分区数据无处安放，会Exception！！！
如果 reduceTask的数量=1，则不管mapTask端输出多少个分区文件，最终结果都交给这一个reduceTask，
最终也就只会产生一个结果文件 part-r-00000.

```
	    //设置reduceTasks进程数量
	    job.setNumReduceTasks(4);
	
	    //设置分区使用的partitioner
	    job.setPartitionerClass(MobilePartioner.class);
```

### 创建分区类,继承Partitioner类，实现getPartition()方法

```
package com.lanou.util;

import java.util.HashMap;
import java.util.Map;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Partitioner;
import com.lanou.model.StreamBean;

public class MobilePartioner extends Partitioner<Text, StreamBean> {
//1. map方法context.write()的key
//2. map方法context.write()的value
//3. reduceTask数量
	private static Map map;
	static{
		map = new HashMap<String,Integer>();
		map.put("134", 0);
		map.put("135", 1);
		map.put("136", 2);
	}
	
	@Override
	public int getPartition(Text paramKey, StreamBean paramValue, int paramInt) {
		// TODO Auto-generated method stub
//		System.out.println("get 134 partition:"+map.get("134"));
//		System.out.println("get 135 partition:"+map.get("135"));
//		System.out.println("get 136 partition:"+map.get("136"));
		String key = paramKey.toString().substring(0,3);
		
//		System.out.println(paramKey);
//		System.out.println(paramValue);
//		System.out.println(paramInt);
		
		Integer result = (Integer) map.get(key);
		
		if (result == null) {
			result = 3;
		}
//		返回值设置数据交给哪一个reduceTask
		return result;
	}
}
```

### Mapper区

```
package com.lanou.util;

import java.io.IOException;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;
import com.lanou.model.StreamBean;

public class BeanStreamMapper extends Mapper<Object, Text, Text, StreamBean > {

	private Text phoneText = new Text();
	
	@Override
	protected void map(Object key, Text value, Mapper<Object, Text, Text, StreamBean>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		
		String[] vals = value.toString().split("\\s+");
		String phone = vals[1];
		String uploatStr = vals[vals.length-3];
		String downloatStr = vals[vals.length-2];
		StreamBean streamBean = new StreamBean(uploatStr,downloatStr);
		phoneText.set(phone);
		context.write(phoneText, streamBean);
	}
}
```

### Reducer区

```
package com.lanou.util;

import java.io.IOException;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Reducer;
import com.lanou.model.StreamBean;

public class BeanStreamReduce extends Reducer<Text, StreamBean, Text, StreamBean >{
	
	@Override
	protected void reduce(Text key, Iterable<StreamBean> lists,
			Reducer<Text, StreamBean, Text, StreamBean>.Context context) throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		int uploadSum = 0;
		int downloadSum = 0;
		for (StreamBean streamBean : lists) {
			
			uploadSum += streamBean.getUploadStream();
			downloadSum += streamBean.getDownloadStream();
		
		}
		StreamBean streamBean = new StreamBean(uploadSum,downloadSum); 
		context.write(key,streamBean );
	}
}
```