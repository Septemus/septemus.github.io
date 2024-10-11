# 西南交通大学数据挖掘作业1-主成分分析


{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2024-2025学年上半学期开设的数据挖掘课程
{{< /admonition >}}

> # 1 作业内容

1. 理解PCA的原理及数学推导
2. 手动实现主成分分析PCA算法，参考算法如下：

<img src="/images/pca.png" width="80%">

> # 2 代码

> ## 2.1 sklearn_pca

```python
def sklearn_pca(data,threshold:float):
    principal=PCA(n_components=threshold) #主成分个数系数
    principal.fit(data)
    x=principal.transform(data)
    return [x,principal.components_]
```

> ## 2.2 手动实现的pca

```python
def manual_pca(data,threshold:float):
    # 计算协方差矩阵
    co_var=np.cov(data,rowvar=False)
    # 求特征根和特征向量
    eigen_values , eigen_vectors=np.linalg.eig(co_var)
    #根据主成分个数系数对特征向量进行筛选
    sorted_index = np.argsort(eigen_values)[::-1]
    sorted_eigenvalue = eigen_values[sorted_index]
    sum=sorted_eigenvalue.sum()
    tmp=0
    count=0
    for v in sorted_eigenvalue:
        tmp+=v
        count+=1
        if(tmp/sum>threshold) :
            break
    sorted_index=sorted_index[:count]
    sorted_eigenvalue=sorted_eigenvalue[:count]
    sorted_eigenvectors = eigen_vectors[:,sorted_index]
    
    # 用特征向量描述原来的矩阵
    X_reduced = np.dot(sorted_eigenvectors.transpose() , data.transpose() ).transpose()

    return [X_reduced,sorted_eigenvectors.transpose()]
```

> ## 2.3 执行

```python
data = pd.read_csv('data-mining/diabetes.csv')
data['Outcome']=data['Outcome'].map({'YES':0,'NO':1}) 
data=(data - data.mean()) / data.std() # z-score标准化

ans1=sklearn_pca(data,threshold)
print("sklearn_pca运行结果：\n")
print("投影矩阵：\n",ans1[1])
print("降维后数据：\n",ans1[0])

# 用散点图可视化sklearn_pca的投影矩阵
plt.figure()
for i in range(ans1[1].shape[0]):
    plt.scatter([i for j in ans1[1][i]],ans1[1][i],c="red")

ans2=manual_pca(data,threshold)
print("manual_pca运行结果：\n")
print("投影矩阵：\n",ans2[1])
print("降维后数据：\n",ans2[0])

# 用散点图可视化manual_pca的投影矩阵
for i in range(ans2[1].shape[0]):
    plt.scatter([i for j in ans2[1][i]],ans2[1][i],c="green",alpha=0.5)

plt.show()
```

> # 3 运行结果

> ## 3.1 输出结果

<img src="/images/data-mining/pca_exp1_res1.png" width="80%">

> ## 3.2 可视化结果

<img src="/images/data-mining/pca_exp1_res2.png" width="80%">

> # 4 源码已上传github

github仓库：
{{< person url="https://github.com/Septemus/swjtu_data_mining_exp1" name="swjtu_data_mining_exp1" text="github库" picture="/images/github.jpg" >}}
