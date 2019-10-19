## 使用kube-init下载数据

[线上数据管理-数据下载]([https://wiki.shannonai.com/books/shannon-%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/page/%E7%BA%BF%E4%B8%8A%E6%95%B0%E6%8D%AE%E7%AE%A1%E7%90%86#bkmrk-%E6%95%B0%E6%8D%AE%E4%B8%8B%E8%BD%BD](https://wiki.shannonai.com/books/shannon-技术文档/page/线上数据管理#bkmrk-数据下载))

1. 修改values.yaml中的kubeInit.enbled的值为true

```yaml
kubeInit:
  enabled: false
  image: "harbor.shannonai.com/public/kube-init:v1.2.4"
  pullPolicy: IfNotPresent
  command: []  # replace entrypoint in image, for example: command: ["echo"]
  args: ["init"] # arguments for entrypoint, for example: args: ["arg1", "arg2"]
```

2. 在templates/configmap.yaml中的data资源下添加要下载的文件url以及指定存放目录.

```yaml
data:
  # 配置文件名称是 data.url, 挂载路径是 conf/data.url
  data.url: |
  	// 示例1	如果仅指定文件url,那么默认下载到data目录下
  	https://files.shannonai.com/index.php/s/CTPMsR4gyrcPjor/download?path=%2Fservice1%2Fv0.0.1&files=file1.txt
  	
  	// 示例2	使用 -> 指定文件夹,必须以/结尾,默认使用远端文件名
  	https://files.shannonai.com/index.php/s/CTPMsR4gyrcPjor/download?path=%2Fservice1%2Fv0.0.1&files=file1.txt -> data1/
    
    // 示例3	使用 -> 指定文件夹和文件名
    https://files.shannonai.com/index.php/s/CTPMsR4gyrcPjor/download?path=%2Fservice1%2Fv0.0.1&files=file1.txt -> data2/fileName.txt
    
    // 注意:每行仅包含一个文件
```

