## join 
#### map端的join（1）（不需要reduce）
#### 把小表分发到map节点缓存中，这样mapper端就可以在本地对自己的大表数据进行join，并输出最终结果，提高join操作并发度，加快处理速度
 	
	mapper区 自定义bean作为key
	setup()只在map初始化上执行一次，在setup中处理缓存文件，直接用本地IO读取（maptask本地工作目录下的一个小文件）
```
	public class JoinMapper extends Mapper<Object, Text, MapJoinBean, NullWritable> {
	private MapJoinBean mapJoinBean = new MapJoinBean();
	//用一个map属性存setup中获取的从表的数据
	private Map<String,MapJoinBean> containMap = new HashMap<>();
	
	//private Text keyText = new Text();
	
	
	//在map之前执行一次
	@Override
	protected void setup(Mapper<Object, Text, MapJoinBean,NullWritable>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		//先按流读可以考虑编码问题
		//Reader可以按行读
		FileInputStream fileInputStream = new FileInputStream("goods.txt");
		BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(fileInputStream));
		String line = null;
		//定义一个容器存获取的数据(map)
		while (StringUtils.isNotEmpty(line = bufferedReader.readLine())) {
			System.out.println("line" + line);
			String[] goods = line.split("\\s+");
			MapJoinBean goodsBean = new MapJoinBean();
			goodsBean.setGoods(goods[0], goods[1], goods[2]);
			containMap.put(goodsBean.getGoodsId(), goodsBean);
		}
		
		//FieldReader fieldReader = new FieldReader("goods.txt", null);
	}
	
	@Override
	protected void map(Object key, Text value, Mapper<Object, Text, MapJoinBean,NullWritable>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		String[] vals = value.toString().split("\\s+");
		mapJoinBean.setOrder(vals[0], vals[2], vals[3]);
		//根据goodsId找到商品进行数据填充
		MapJoinBean goodsBean = containMap.get(mapJoinBean.getGoodsId());
		mapJoinBean.setGoods(goodsBean.getGoodsName(), goodsBean.getStockCount());
		//keyText.set(mapJoinBean.getGoodsId());
		context.write(mapJoinBean,NullWritable.get());
	}
}
```
	driver区将hdfs上数据放入缓存
```	
	job.addCacheFile(new URI("hdfs://172.18.24.195:9000/input/goods.txt"));
```
  
## map端的join（2）（需要reduce）
 
	bean
```
@Override
	public void readFields(DataInput input) throws IOException {
		// TODO Auto-generated method stub
		this.orderId = input.readInt();
		this.goodsId = input.readUTF();
	}
	@Override
	public void write(DataOutput output) throws IOException {
		// TODO Auto-generated method stub
		output.writeInt(this.orderId);
		output.writeUTF(this.goodsId);
	}
	@Override
	public int compareTo(MapJoinBean arg0) {
		// TODO Auto-generated method stub
		//先按orderID排序再按goodsID排序
		int result = - (this.getOrderId()-arg0.getOrderId());
		if (result == 0) {
			result = - this.getGoodsId().compareTo(arg0.getGoodsId());
		}
		return result;
	}
```

	mapper端 
	setup同（1）中的setup
	map 把自定义bean作为value
```
protected void map(Object key, Text value, Mapper<Object, Text, Text, MapJoinBean>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		String[] vals = value.toString().split("\\s+");
		mapJoinBean.setOrder(vals[0], vals[2], vals[3]);
		//根据goodsId找到商品进行数据填充
		MapJoinBean goodsBean = containMap.get(mapJoinBean.getGoodsId());
		mapJoinBean.setGoods(goodsBean.getGoodsName(), goodsBean.getStockCount());
		keyText.set(mapJoinBean.getGoodsId());
		context.write(keyText, mapJoinBean);
	}
```
      
* reducer端
```
@Override
	protected void reduce(OrderInfo orderInfo, Iterable<NullWritable> arg1,
			Reducer<OrderInfo, NullWritable, OrderInfo, NullWritable>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		context.write(orderInfo, NullWritable.get());
	}  
```	
 * 小结
 
    ![image.png](https://upload-images.jianshu.io/upload_images/14466577-4368d0de22ea8d79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
