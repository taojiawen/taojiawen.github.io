## join 
#### map�˵�join��1��������Ҫreduce��
#### ��С��ַ���map�ڵ㻺���У�����mapper�˾Ϳ����ڱ��ض��Լ��Ĵ�����ݽ���join����������ս�������join���������ȣ��ӿ촦���ٶ�
 	
	mapper�� �Զ���bean��Ϊkey
	setup()ֻ��map��ʼ����ִ��һ�Σ���setup�д������ļ���ֱ���ñ���IO��ȡ��maptask���ع���Ŀ¼�µ�һ��С�ļ���
```
	public class JoinMapper extends Mapper<Object, Text, MapJoinBean, NullWritable> {
	private MapJoinBean mapJoinBean = new MapJoinBean();
	//��һ��map���Դ�setup�л�ȡ�Ĵӱ������
	private Map<String,MapJoinBean> containMap = new HashMap<>();
	
	//private Text keyText = new Text();
	
	
	//��map֮ǰִ��һ��
	@Override
	protected void setup(Mapper<Object, Text, MapJoinBean,NullWritable>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		//�Ȱ��������Կ��Ǳ�������
		//Reader���԰��ж�
		FileInputStream fileInputStream = new FileInputStream("goods.txt");
		BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(fileInputStream));
		String line = null;
		//����һ���������ȡ������(map)
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
		//����goodsId�ҵ���Ʒ�����������
		MapJoinBean goodsBean = containMap.get(mapJoinBean.getGoodsId());
		mapJoinBean.setGoods(goodsBean.getGoodsName(), goodsBean.getStockCount());
		//keyText.set(mapJoinBean.getGoodsId());
		context.write(mapJoinBean,NullWritable.get());
	}
}
```
	driver����hdfs�����ݷ��뻺��
```	
	job.addCacheFile(new URI("hdfs://172.18.24.195:9000/input/goods.txt"));
```
  
## map�˵�join��2������Ҫreduce��
 
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
		//�Ȱ�orderID�����ٰ�goodsID����
		int result = - (this.getOrderId()-arg0.getOrderId());
		if (result == 0) {
			result = - this.getGoodsId().compareTo(arg0.getGoodsId());
		}
		return result;
	}
```

	mapper�� 
	setupͬ��1���е�setup
	map ���Զ���bean��Ϊvalue
```
protected void map(Object key, Text value, Mapper<Object, Text, Text, MapJoinBean>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		String[] vals = value.toString().split("\\s+");
		mapJoinBean.setOrder(vals[0], vals[2], vals[3]);
		//����goodsId�ҵ���Ʒ�����������
		MapJoinBean goodsBean = containMap.get(mapJoinBean.getGoodsId());
		mapJoinBean.setGoods(goodsBean.getGoodsName(), goodsBean.getStockCount());
		keyText.set(mapJoinBean.getGoodsId());
		context.write(keyText, mapJoinBean);
	}
```
      
* reducer��
```
@Override
	protected void reduce(OrderInfo orderInfo, Iterable<NullWritable> arg1,
			Reducer<OrderInfo, NullWritable, OrderInfo, NullWritable>.Context context)
			throws IOException, InterruptedException {
		// TODO Auto-generated method stub
		context.write(orderInfo, NullWritable.get());
	}  
```	
 * С��
 
    ![image.png](https://upload-images.jianshu.io/upload_images/14466577-4368d0de22ea8d79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
