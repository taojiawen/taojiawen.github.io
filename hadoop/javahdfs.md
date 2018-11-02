# Java操作hdfs代码
```
package com.lanou.test;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URI;
import java.net.URISyntaxException;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.BlockLocation;
import org.apache.hadoop.fs.FSDataInputStream;
import org.apache.hadoop.fs.FSDataOutputStream;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.LocatedFileStatus;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.RemoteIterator;
import org.apache.hadoop.io.IOUtils;
import org.junit.Before;
import org.junit.Test;

public class HDFSTest2 {
	private static FileSystem fileSystem;
	
	//创建文件夹
	@Test
	public void mkdirs() throws IOException {
		
		fileSystem.mkdirs(new Path("/list/"));
	}
	//上传文件
	@Test
	public void upload() throws IOException {
		
		fileSystem.copyFromLocalFile(new Path("D:/hehe/hadoop-2.7.3.tar.gz"), new Path("/list"));
	}
	//下载文件
	@Test
	public void Download() throws IllegalArgumentException, IOException{
		
		fileSystem.copyToLocalFile(false, new Path("/taobao/java.md"), new Path("D:/hdfs/output/"), true);
	}
	//删除文件
	@Test
	public void delete() throws IllegalArgumentException, IOException{
		fileSystem.delete(new Path("/taobao"),false);
	}
	//查看文件信息
	@Test
	public void findInfo() throws FileNotFoundException, IllegalArgumentException, IOException{
		//迭代器
		RemoteIterator<LocatedFileStatus> listFiles = fileSystem.listFiles(new Path("/list"), true);
//		User user = new User();
//		user.setUserId(123);
//		user.setPassword("asd");
//		user.setUsername("as");
//		System.out.println(user);
//		System.out.println(user.toString());
		while (listFiles.hasNext()) {
			LocatedFileStatus next = (LocatedFileStatus) listFiles.next();
			BlockLocation[] blockLocations = next.getBlockLocations();
			for (BlockLocation blockLocation : blockLocations) {
				System.out.println(blockLocation);
			}
			System.out.println(next);
		}
	}
	//流上传文件
	@Test
	public void uploadByStream() throws IllegalArgumentException, IOException{
		//input
		FileInputStream fileInputStream = new FileInputStream("D:/hehe/eclipse-jee-neon-3-win32-x86_64.zip");
		//output
		FSDataOutputStream hdfsOutputStream = fileSystem.create(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"));
		IOUtils.copyBytes(fileInputStream,hdfsOutputStream, 4096);
	}
	//流下载文件
	@Test
	public void downloadByStream() throws IllegalArgumentException, IOException{
		
		FSDataInputStream inputStream = fileSystem.open(new Path("/list/in.txt"));
		FileOutputStream fileOutputStream = new FileOutputStream("D:/hdfs/output/in.txt");
		org.apache.commons.io.IOUtils.copy(inputStream,fileOutputStream);
	}
	//seek偏移下载
	@Test
	public void downloadBySeek() throws IllegalArgumentException, IOException{
		
		FSDataInputStream inputStream = fileSystem.open(new Path("/list/hadoop-2.7.3.tar.gz"));
		//偏移
		inputStream.seek(10);
		FileOutputStream fileOutputStream = new FileOutputStream("D:/hdfs/output/out.txt");
		org.apache.commons.io.IOUtils.copy(inputStream,fileOutputStream);
	}
	//只有两个block块下载第二个block块
	@Test
	public void downloadBlock() throws FileNotFoundException, IllegalArgumentException, IOException{
		FSDataInputStream inputStream = fileSystem.open(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"));
		RemoteIterator<LocatedFileStatus> listFiles = fileSystem.listFiles(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"), false);
		while (listFiles.hasNext()) {
			LocatedFileStatus next = (LocatedFileStatus) listFiles.next();
			BlockLocation[] blockLocations = next.getBlockLocations();
			for (int i = 0; i < blockLocations.length; i++) {
				System.out.println(blockLocations[i].getOffset());
				if (i==1) {
					
					inputStream.seek(blockLocations[i].getOffset());
					break;
				}
			}
		}
		
		FileOutputStream fileOutputStream = new FileOutputStream("D:/hdfs/output/block2.zip");
		org.apache.commons.io.IOUtils.copy(inputStream,fileOutputStream);
	}
	//两个以上block块下载第二个
	@Test
	public void copyLargeBlock() throws FileNotFoundException, IllegalArgumentException, IOException{
		FSDataInputStream inputStream = fileSystem.open(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"));
		FileOutputStream fileOutputStream = new FileOutputStream("D:/hdfs/output/block2.zip");
		RemoteIterator<LocatedFileStatus> listFiles = fileSystem.listFiles(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"), false);
		while (listFiles.hasNext()) {
			LocatedFileStatus next = (LocatedFileStatus) listFiles.next();
			BlockLocation[] blockLocations = next.getBlockLocations();
			for (int i = 0; i < blockLocations.length; i++) {
				System.out.println(blockLocations[i].getOffset());
				if (i==1) {
					long inputoffset = blockLocations[i].getOffset();
					long length = blockLocations[1].getLength();
					org.apache.commons.io.IOUtils.copyLarge(inputStream, fileOutputStream, inputoffset, length);
					break;
				}
			}
		}
	}
	//两个以上block块下载每个block块
	@Test
	public void copyLargeEachBlock() throws FileNotFoundException, IllegalArgumentException, IOException{
		
		
		RemoteIterator<LocatedFileStatus> listFiles = fileSystem.listFiles(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"), false);
		while (listFiles.hasNext()) {
			LocatedFileStatus next = (LocatedFileStatus) listFiles.next();
			BlockLocation[] blockLocations = next.getBlockLocations();
			FSDataInputStream inputStream = fileSystem.open(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"));
			for (int i = 0; i < blockLocations.length; i++) {
				//inputStream.seek(0);
				FileOutputStream fileOutputStream = new FileOutputStream("D:/hdfs/output/blocks"+(i+01)+".zip");
				System.out.println(blockLocations[i].getOffset());
				//long inputoffset = blockLocations[i].getOffset();
				long length = blockLocations[i].getLength();
				
				org.apache.commons.io.IOUtils.copyLarge(inputStream, fileOutputStream, 0, length);
					
			}
		}
	}
	//用io流两个以上block块下载每个block块
	@Test
	public void copyIOEachBlock() throws FileNotFoundException, IllegalArgumentException, IOException{
		
		
		RemoteIterator<LocatedFileStatus> listFiles = fileSystem.listFiles(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"), false);
		while (listFiles.hasNext()) {
			LocatedFileStatus next = (LocatedFileStatus) listFiles.next();
			BlockLocation[] blockLocations = next.getBlockLocations();
			long offset = 0;
			FSDataInputStream inputStream = fileSystem.open(new Path("/list/eclipse-jee-neon-3-win32-x86_64.zip"));
			for (int i = 0; i < blockLocations.length; i++) {
				
				FileOutputStream fileOutputStream = new FileOutputStream("D:/hdfs/output/blocks"+(i+1)+".zip");
			
				long inputoffset = blockLocations[i].getOffset();
				System.out.println(inputoffset);
				long length = blockLocations[i].getLength();
				System.out.println(length);
				
				byte[] b = new byte[4096];
				int numberRead = 0;
				
				while((numberRead = inputStream.read(b)) != -1 ) {
					
					offset = offset+numberRead; 
					fileOutputStream.write(b,0,numberRead);
					if (offset == length+inputoffset ) {
						break;
					}
				}	
				
				fileOutputStream.close();
			}
			inputStream.close();
		}
	
	}
	//连接hdfs
	@Before
	public void befores() throws IOException, URISyntaxException, InterruptedException{
		
//		Configuration configuration = new Configuration();
//		//设置要使用的文件系统是hdfs -> 地址为.....
		//设置用户
//		System.setProperty("HADOOP_USER_NAME", "hadoop");
//		configuration.set("fs.defaultFS", "hdfs://172.18.24.195:9000");
//		fileSystem = FileSystem.get(configuration);
//		System.out.println(fileSystem);
		
		Configuration configuration = new Configuration();
        // Hadoop的用户名
        String hdfsUserName = "hadoop";
        
        // HDFS的访问路径
        URI hdfsUri = new URI("hdfs://172.18.24.195:9000");
         
        // 根据远程的NN节点，获取配置信息，创建HDFS对象
        fileSystem = FileSystem.get(hdfsUri,configuration,hdfsUserName);
        
	}
}
```