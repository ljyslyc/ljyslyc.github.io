---
layout: post
title: "Pytorch学习07"
date: 2019-08-11
categories: Pyorch Python
tags: Pyorch Python
excerpt: pytorch初始化
mathjax: true
author: LJY
---
* content
{:toc}

# nn.Parameter

` nn.Parameter 包裹起来才能加入model.parameters()中，才能够使用优化器进行优化参数`

```python
x = torch.from_numpy(x).float()
y = torch.from_numpy(y).float()
# w,b可以被优化器进行优化
w = nn.Parameter(torch.randn(2, 1))
b = nn.Parameter(torch.zeros(1))

optimizer = torch.optim.SGD([w, b], 1e-1)

def logistic_regression(x):
    return torch.mm(x, w) + b

criterion = nn.BCEWithLogitsLoss()
for e in range(100):
    out = logistic_regression(x)
    loss = criterion(out, y)
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
    if (e + 1) % 20 == 0:
        print('epoch: {}, loss: {}'.format(e+1, loss.data[0]))
```



## 自定义网络层和函数

```python
import  torch
from    torch import nn
from    torch import optim


# nn.Parameter 包裹起来才能加入model.parameters()中，才能够使用优化器进行优化参数
class MyLinear(nn.Module):
    def __init__(self, inp, outp):
        super(MyLinear, self).__init__()

        # requires_grad = True
        self.w = nn.Parameter(torch.randn(outp, inp))
        self.b = nn.Parameter(torch.randn(outp))
 	# x.shape [batch,inp]
    def forward(self, x):
        # x = x @ self.w.t() + self.b
        x = x.mm(self.w.t()) + self.b
        # .t()为转置  @等价于mm均为矩阵乘法
        return x
    
    
# 类函数，可以写在Sequential中
class Flatten(nn.Module):

    def __init__(self):
        super(Flatten, self).__init__()

    def forward(self, input):
        return input.view(input.size(0), -1)
```

## 访问children/modules

```
class sim_net(nn.Module):
    def __init__(self):
        super(sim_net, self).__init__()
        self.l1 = nn.Sequential(
            nn.Linear(30, 40),
            nn.ReLU()
        )
        
        self.l1[0].weight.data = torch.randn(40, 30) # 直接对某一层初始化
        
        self.l2 = nn.Sequential(
            nn.Linear(40, 50),
            nn.ReLU()
        )
        
        self.l3 = nn.Sequential(
            nn.Linear(50, 10),
            nn.ReLU()
        )
    
    def forward(self, x):
        x = self.l1(x)
        x =self.l2(x)
        x = self.l3(x)
        return x
net2 = sim_net()

# 访问 children
for i in net2.children():
    print(i)
    
# 访问 modules
for i in net2.modules():
    print(i)
```



```python
class BasicNet(nn.Module):

    def __init__(self):
        super(BasicNet, self).__init__()

        self.net = nn.Linear(4, 3)

    def forward(self, x):
        return self.net(x)

class Net(nn.Module):

    def __init__(self):
        super(Net, self).__init__()

        self.net = nn.Sequential(BasicNet(),
                                 nn.ReLU(),
                                 nn.Linear(3, 2))

    def forward(self, x):
        return self.net(x)
        
net = Net()
net.to(device)

net.train()
net.eval()

# net.load_state_dict(torch.load('ckpt.mdl'))
# torch.save(net.state_dict(), 'ckpt.mdl')

for name, t in net.named_parameters():
    print('parameters:', name, t.shape)
print("-"*20)
# 找到直系孩子
for name, m in net.named_children():
    print('children:', name, m)
print("-"*20)
#找到所有的孩子，包括孩子的孩子
for name, m in net.named_modules():
    print('modules:', name, m)


parameters: net.0.net.weight torch.Size([3, 4])
parameters: net.0.net.bias torch.Size([3])
parameters: net.2.weight torch.Size([2, 3])
parameters: net.2.bias torch.Size([2])
--------------------
children: net Sequential(
  (0): BasicNet(
    (net): Linear(in_features=4, out_features=3, bias=True)
  )
  (1): ReLU()
  (2): Linear(in_features=3, out_features=2, bias=True)
)
--------------------
modules:  Net(
  (net): Sequential(
    (0): BasicNet(
      (net): Linear(in_features=4, out_features=3, bias=True)
    )
    (1): ReLU()
    (2): Linear(in_features=3, out_features=2, bias=True)
  )
)
# 模型本身

modules: net Sequential(
  (0): BasicNet(
    (net): Linear(in_features=4, out_features=3, bias=True)
  )
  (1): ReLU()
  (2): Linear(in_features=3, out_features=2, bias=True)
)
# 直系孩子
modules: net.0 BasicNet(
  (net): Linear(in_features=4, out_features=3, bias=True)
)
# 孩子的孩子
modules: net.0.net Linear(in_features=4, out_features=3, bias=True)
# 
modules: net.1 ReLU()
modules: net.2 Linear(in_features=3, out_features=2, bias=True)
```


