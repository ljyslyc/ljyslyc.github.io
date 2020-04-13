---
layout: post
title: "Pytorch学习08"
date: 2019-08-13
categories: Pyorch Python
tags: Pyorch Python
excerpt: 自定义网络层
mathjax: true
author: LJY
---
* content
{:toc}

网络的保存和提取有两种方式：一种是保存网络的状态（parameters and buffers）；另一种是保存整个网络（模型和状态）,当然是推荐第一种啦！！！(方便重构)。
官方保存模型讲解：
https://pytorch.org/tutorials/beginner/saving_loading_models.html

## 1 保存参数

    # 保存模型
    torch.save(model.state_dict(), "wordavg-model.pth")
    
    # 加载模型，加载前需要定义模型的结构
    model = WordAVGModel(vocab_size=VOCAB_SIZE, 
                         embedding_size=EMBEDDING_SIZE, 
                         output_size=OUTPUT_SIZE, 
                         pad_idx=PAD_IDX)
    model = model.cuda()
    # 将state_dict中的参数和缓冲区复制到模型中
    model.load_state_dict(torch.load("wordavg-model.pth"))

在PyTorch中，torch.nn.Module模型的可学习参数（即权重和偏差）包含在模型的参数中（使用model.parameters（）访问）。 state_dict只是一个Python字典对象，它将每个图层映射到其参数张量。 请注意，只有具有可学习参数（卷积层，线性层等）和已注册缓冲区（batchnorm的running_mean）的图层在模型的state_dict中具有条目。 优化器对象（torch.optim）也有一个state_dict，它包含有关优化器状态的信息，以及使用的超参数。

因为state_dict对象是Python字典，所以它们可以轻松保存，更新，更改和恢复，为PyTorch模型和优化器添加了大量模块化。

## 2 整个模型

    Save:
    torch.save(model, PATH)
    Load:
    # Model class must be defined somewhere
    model = torch.load(PATH)
    model.eval()
这种方式仅看文档的写法，会给你造成一个误解，认为整个模型保存下来了，任何地方都能直接load使用，其实不然！！！

此保存/加载过程使用最直观的语法并涉及最少量的代码。 以这种方式保存模型将使用Python的pickle模块保存整个模块。 这种方法的缺点是序列化数据绑定到特定类以及保存模型时使用的确切目录结构。 这是因为pickle不保存模型类本身。 相反，它会保存包含类的文件的路径，该文件在加载时使用。 因此，当您在其他项目中或在重构之后使用时，您的代码可能会以各种方式中断。

常见的PyTorch约定是使用.pt或.pth文件扩展名保存模型。

请记住，在运行推理之前，必须调用model.eval（）将dropout和批处理规范化层设置为评估模式。 如果不这样做，将导致不一致的推理结果。

## 3 Saving & Loading a General Checkpoint for Inference and/or Resuming Training

    Save:
    torch.save({
                'epoch': epoch,
                'model_state_dict': model.state_dict(),
                'optimizer_state_dict': optimizer.state_dict(),
                'loss': loss,
                ...
                }, PATH)
    Load:
    model = TheModelClass(*args, **kwargs)
    optimizer = TheOptimizerClass(*args, **kwargs)
    
    checkpoint = torch.load(PATH)
    model.load_state_dict(checkpoint['model_state_dict'])
    optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
    epoch = checkpoint['epoch']
    loss = checkpoint['loss']
    
    model.eval()
    # - or -
    model.train()