# 分组 

## driver区

```
	job.setGroupingComparatorClass(GroupByOrderComparator.class);
```

## 自定义GroupingComparator

```
package com.lanou.util;

import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.WritableComparator;
import com.lanou.bean.OrderInfo;

public class GroupByOrderComparator extends WritableComparator  {
	
	//构造时直接调用
	protected GroupByOrderComparator() {
		// TODO Auto-generated constructor stub
		super(OrderInfo.class,true);
	}
	@Override
	//返回0则分为一组进入一个reduce
	public int compare(WritableComparable a, WritableComparable b) {
		// TODO Auto-generated method stub
		OrderInfo orderInfo1 = (OrderInfo)a;
		OrderInfo orderInfo2 = (OrderInfo)b;
		//orerid 相同分为一组
		int compareTo = orderInfo1.getOrderId().compareTo(orderInfo2.getOrderId());
 		return compareTo;
	}
}
```
	分组前提要先排序(因为分组只比较相邻的对象 直到返回不是0就进入reduce)

	bean 重写 compareTo()方法
```
	@Override
	public int compareTo(OrderInfo o) {
		// TODO Auto-generated method stub
		int res = orderId.compareTo(o.getOrderId());
		if(res == 0 ){
			res = price.compareTo(o.getPrice());
		}
		return res;
	}
```
	mapper区 对想要的数据进行获取封装
```
@Override
	protected void map(Object key, Text value, Mapper<Object, Text, Text, OrderInfo>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		String[] vals = value.toString().split("\\s+");
		orderinfo.setOrder(vals[0], vals[1], vals[2]);
		ordeText.set(orderinfo.getOrderId());
		context.write(ordeText, orderinfo);
	}
```

	reducer区 对已经分好组的数据进行比较 最后输出
```
@Override
	protected void reduce(Text orderId, Iterable<OrderInfo> orderList, Reducer<Text, OrderInfo, OrderInfo, NullWritable>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		OrderInfo maxOrder = new OrderInfo();
		for (OrderInfo orderInfo : orderList) {
			
			if (orderInfo.getPrice() > maxOrder.getPrice()) {
				//深拷贝
				try {
					BeanUtils.copyProperties(maxOrder, orderInfo);
				} catch (IllegalAccessException | InvocationTargetException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
		context.write(maxOrder, NullWritable.get());
	}
```