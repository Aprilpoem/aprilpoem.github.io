---
title: Image | numpy | tensor图像转换问题
date: 2019-1-3 22：33：00
tags: numpy,Image
---

## Image | numpy | tensor图像转换问题
python还是不太熟练，已经在这里栽过很多次了，索性整理一下

#### narray and PIL

PIL to narray:` narray = np.array(PIL_image)`
```python
In [10]: from PIL import Image                                                  

In [11]: import numpy as np                                                     

In [12]: import os                                                              

In [13]: images = os.listdir()                                                  

In [14]: tmp = Image.open(images[0])                                            

In [15]: tmp # WxH: 700x65                                                                  
Out[15]: <PIL.PpmImagePlugin.PpmImageFile image mode=RGB size=700x605 at 0x7F9196A93748>

In [16]: np_tmp = np.array(tmp.convert('RGB')) #HxWx3                               

In [17]: np_tmp.shape                                                           
Out[17]: (605, 700, 3)

```
narray to PIL `Image.fromarray(numpy_data)`
```python
In [18]: tmp_PIL=Image.fromarray(np_tmp)                                        

In [19]: type(tmp_PIL)                                                          
Out[19]: PIL.Image.Image

In [20]: tmp_PIL.show() 
```

#### numpy and tensor
numpy to tensor  `tensor_tmp = torch.from_numpy(np_tmp)`
```python
In [27]: tensor_tmp.shape                                                       
Out[27]: torch.Size([605, 700, 3])
```
tensor to numpy `np_tmp = tensor_tmp.numpy()`
```python
In [28]: type(tensor_tmp.numpy())                                               
Out[28]: numpy.ndarray

```
#### Tensor and PIL
[Transforms on PIL Image](https://pytorch.org/docs/stable/torchvision/transforms.html#transforms-on-pil-image)
`torchvision.transforms`操作是对PIL image进行的

PIL.Image to Tensor
```python
In [33]: simple_transform=tfs.Compose([ 
    ...: tfs.ToTensor(),#range[0,255]->[0.0,1.0] 
    ...: ])                                                                     

In [34]: tmp                                                                    
Out[34]: <PIL.PpmImagePlugin.PpmImageFile image mode=RGB size=700x605 at 0x7F9196A93748>

In [35]: tmp.show()                                                             

In [36]: tensor_tmp_0 = simple_transform(tmp)                                   

In [37]: tensor_tmp_0.shape                                                     
Out[37]: torch.Size([3, 605, 700])#3xHxW

```
Tensor to numpy.narray and show it
```python
In [38]: np_tmp_0 = tensor_tmp_0.numpy()*255                                    

In [39]: img_0 = np_tmp_0.astype('uint8')                                       

In [40]: img_0 = np.transpose(img_0,(1,2,0)) #维度0（也就是3）放到了最后面                                   

In [41]: img_0.shape                                                            
Out[41]: (605, 700, 3)#np.array格式用opencv-python里的cv2.imshow(img)

```
Tensor to PIL
`tmp_img = tfs.ToPILImage()(tensor_tmp_0)`
```python
In [9]: t_img.shape                                                             
Out[9]: torch.Size([3, 605, 700])

```

---
常用转换搭配：
当从隐藏层提取feature maps,需要可视化为图片时，可以：
Tensor -> numpy (注意一下通道的转换，cv2.imsave)
