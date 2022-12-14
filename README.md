# CV - ActionUnderstanding - Survey - By YK

## Related Papers
### Action Recognition
- Revisiting Skeleton-based Action Recognition (**CVPR 2022**) [[PDF](https://openaccess.thecvf.com/content/CVPR2022/papers/Duan_Revisiting_Skeleton-Based_Action_Recognition_CVPR_2022_paper.pdf)] [[Github](https://github.com/kennymckormick/pyskl)]
    - 新的基于骨骼的动作识别方法POSeconv3D(relies on a 3D heatmap volume instead of a graph sequence as the base representation ofhuman skeletons)
    - 与基于GCN的方法相比,Poseconv3D在学习时空特征方面更有效，对姿态估计噪声的鲁棒性更强，并在跨数据集环境下具有更好的泛化能力
    - 此外，Poseconv3D可以处理多人场景，而无需额外的计算成本
    - GCN方法在以下几个方面存在局限性：（1）鲁棒性：GCN直接处理人体关节坐标时，其识别能力受到坐标分布偏移的影响，当采用不同的位姿估计器获取坐标时，常常会出现这种情况。 坐标上的一个小扰动往往会导致完全不同的预测(KDD-2019,[[PDF](https://dl.acm.org/doi/pdf/10.1145/3292500.3330851?casa_token=npPj2EW6VRUAAAAA:_Hf_C_XwfP6tMX8SBpQe5Pf3wHwEipMnZIcKUhHppZ23O_3rpZIltd1EcxbWXIqQax-PuilYBz3BDQ))]
    - (2)互操作性：以前的研究表明，不同模态的表征，如RGB、光流和骨架，是互补的。 因此，这些模式的有效组合通常可以导致动作识别的性能提升。 然而，GCN是在不规则的骨架图上运行的，这使得它很难与通常在规则网格上表示的其他模式融合，尤其是在早期阶段
    - (3）可扩展性：另外，由于GCN将每个人体关节视为一个节点，GCN的复杂度与人数成线性关系，限制了其适用于涉及多人的场景，如群体活动识别
    - 输入为姿态提取后的2D骨骼数据（如果是3D骨骼，则可以拆分为(x,y)(x,z)(y,z)三个2D骨骼）, 然后将不同时间步长的热图沿时间维叠加，形成3D热图体（T*H*W）输入3D CNN
    - 3D HeatMap Volumes对上游姿态估计更鲁棒：我们经验发现，Poseconv3D在不同方法获得的输入骨架上具有很好的泛化能力
    - 另外，Poseconv3D依赖于基本表示的热图，它享受了卷积网络体系结构的最新进展，并且更容易与其他模式集成到多流卷积网络中。 这一特性为进一步提高识别性能打开了很大的设计空间
    - ![poseconv3d](./PoseConv3D.png)
- Fine-grained Action Recognition with Robust Motion Representation Decoupling and Concentration (**ACM MM 2022**) [[PDF](https://dl.acm.org/doi/pdf/10.1145/3503161.3548046?casa_token=r5NidEgxb1sAAAAA:6Q6g1Ye4i30UfGZu6vibCuAnIVBrWOB48ecwzUJ5SATZ9tUIyVNVvAo5h8oyfaye1-jbPGH6G6EzLQ)]
    - 现有的方法通常侧重于时空特征提取和长时间建模，以刻画细粒度行为的复杂时空模式
    - 现有动作数据集中的大多数运动信息难以标注，训练一个具有详细运动级别注释（如姿势注释）的模型代价高昂，甚至不可能
    - 考虑到类内差异较大，类间差异较小，如何从运动表征中识别出与动作相关的特征是细粒度动作识别的关键
    - 然而，在没有显式运动建模的情况下，学习到的时空特征可能更多地强调视觉外观而不是运动(on visual appearance than on motion)，这可能会影响细粒度时间推理所需的有效运动特征的学习![image](https://user-images.githubusercontent.com/71006202/201815815-bfcc7220-0ef4-48ad-a36e-6bc6463b8775.png)
    - 提出了一种运动表示解耦和集中网络(MDCNet)来解决这两个关键问题:(1)如何将健壮的运动表示从时空特征中分离出来;(2)并进一步有效地利用它们来增强识别特征的学习
    - 方法:(1)设计了一个运动表示解耦(MRD)模块，通过视频和片段视图的对比学习，将时空表示分解为外观和运动特征;(2)在提出的运动表示集中(MRC)模块中，进一步利用解耦的运动表示来学习跨每个动作类的所有实例共享的通用运动原型;(3)将解耦后的运动特征通过语义关系投射到所有的运动原型上，得到每个动作类的集中的动作相关特征，有效地刻画细粒度动作的时间差异，提高识别性能![image](https://user-images.githubusercontent.com/71006202/201815867-3613a4a7-da96-4dc0-aa90-28b5660e316b.png)

   
- GRAPH CONTRASTIVE LEARNING FOR SKELETON-BASED ACTION RECOGNITION(**ICLR 2023**) [[PDF](https://openreview.net/pdf?id=PLUXnnxUdr4)]
    - 基于骨架的动作识别领域，目前性能最好的图卷积网络利用序列内上下文构造自适应图进行特征聚集,但这种上下文仍然是局部的，因为丰富的交叉序列关系尚未得到明确的研究
    - ![image](https://user-images.githubusercontent.com/71006202/201863038-4e6336a5-2ee8-4c3d-8d95-2b4b9e8ef4a8.png)
    - 提出了一个基于骨骼的动作识别的图对比学习框架（SkeletongCL）来探索所有序列的全局上下文
    - SkeletongCL通过加强图的类区分性，即类内紧凑性和类间离散性，将图学习跨序列关联起来，提高了GCN区分各种行为模式的能力
    - 还设计了两个记忆库，从实例和语义两个互补的层次丰富跨序列上下文，实现了多上下文尺度下的图对比学习
    - keletongCL建立了一个新的训练范式，并可以无缝地融入现有的GCNS。 在不丧失通用性的情况下，我们将SkeletongCL与三个GCN(2S-ACGN、CTR-GCN和INFOGCN)结合起来，在NTU60、NTU120和NW-UCLA基准上实现了一致的改进
    - ![image](https://user-images.githubusercontent.com/71006202/201863322-ee42b89e-a128-42d8-b940-ceb79b2395f2.png)
    - 我们的方法与它们的不同之处在于：（1）以前的方法像采用集合特征向量来进行对比学习，其中丢失了骨骼中的结构属性。相比之下，SkeletongCL使用图形进行对比，它维护了骨架的结构细节，并提供了关节之间的高阶连接信息。
    - （2）以往的方法只使用存储库来存储实例级表示。 不同的是，我们的内存库存储实例级和语义级表示，允许我们利用单个序列和特定于类的聚合中的上下文，这两者是相互补充的。
    - （3）在预训练阶段使用了以往的方法，而SkeletongCL则被引入到全监督环境中，无需额外的预训练成本。 

- HOW HELPFUL ARE CURRENT GRAPH MODELS FOR SKELETON-BASED ACTION RECOGNITION? A TOPOLOGY AGNOSTIC APPROACH (**ICLR 2023**) [[PDF](https://openreview.net/pdf?id=PbXfwJEyKXT)]
    - 虽然基于GCN的方法不断建立新的最先进的结果，但所提出的体系结构随着各种附加组件而变得越来越复杂
    - 最近的许多工作试图放松GCN框架的拓扑限制，如局部/稀疏连接和置换不变性。然而，在这样的框架下进一步创新的空间极其有限
    - 提出了拓扑不可知网络(TOANET)，这是一个简单的体系结构，仅基于全连接(FC)层，而不是基于骨架的动作识别的GCNS。 它是通过以交替的方式链接应用于跨关节（聚合关节信息）和每个关节内（转换关节特征）的FC层来构建的
    - ToaNet被证明是一个学习人体骨骼数据联合共现的强大体系结构。 ToaNet在NTU RGB+D、NTU RGB+D120和NW-UCLA数据集上取得了更好或可比的结果
    - 我们希望我们的工作能促进对非GCN方法的进一步研究，消除拓扑结构的限制。
    - ![image](https://user-images.githubusercontent.com/71006202/201864566-c613693c-8e11-4dae-9e53-e8db3dad6352.png)
    - 我们贡献了一个纯粹基于全连通层的模型，用于基于骨骼的人类行为识别的空间建模，称为TOANET，提出了一种学习人体关节间多关系交互的新设计。
    - ![image](https://user-images.githubusercontent.com/71006202/201864864-b2c2311e-77af-4881-b90d-3346bbaae162.png)
    - ![image](https://user-images.githubusercontent.com/71006202/201864903-e220683c-e7ab-4ea9-98d0-85fd2c1c1dd6.png)



- HOW HELPFUL ARE CURRENT GRAPH MODELS FOR SKELETON-BASED ACTION RECOGNITION? A TOPOLOGY AGNOSTIC APPROACH (**ICLR 2023**) [[PDF](https://openreview.net/pdf?id=PbXfwJEyKXT)]

### Action Parsing
-  Intra- and Inter-Action Understanding via Temporal Action Parsing (**CVPR 2020**) [[PDF](http://openaccess.thecvf.com/content_CVPR_2020/papers/Shao_Intra-_and_Inter-Action_Understanding_via_Temporal_Action_Parsing_CVPR_2020_paper.pdf)] [[Project](https://sdolivia.github.io/TAPOS/)]
    - [**TAPOS**], a new dataset developed on sport videos with manual annotations of **sub-actions**, and conduct a study on temporal **action parsing** on top 构建的数据集包含了21个奥运体育类中的16K多个动作实例.特点：有一致和干净的背景，多样的内部结构和丰富的子动作
    - 观察到人类对子动作的边界很敏感，即使不知道它们的类别
    - 以高质量的时间分段的形式提供了动作内注释，而不是子动作标签.时间分段将动作划分为不同子动作的片段，隐含地揭示了动作的内部结构，即动作实例是如何由子动作构成的，以及动作间信息，即一个特定的子动作可能共同出现在不同的动作中
    - 进一步在TAPOS上开发了一个改进的时态动作解析框架（基于Transformers,Nips 2017,[PDF](https://proceedings.neurips.cc/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf))，采用两个堆叠的转换器作为核心，以动作实例帧作为查询，以存储体中的参数作为键和值。新的框架在时间动作分析上优于基线，它的结构也使它能够以无监督的方式发现一个动作类内和不同动作类之间的子动作段的语义相似性。通过对透明器的研究，我们还可以揭示额外的动作内信息（例如，哪个子动作对某个动作类别的区分度最高）和动作间信息（例如，哪个子动作通常出现在不同的动作类别中）
    - ![image](https://user-images.githubusercontent.com/71006202/201814197-40a8305e-643b-456e-a0dd-5070e04aaad0.png)

    - 进一步在TAPOS上开发了一个改进的时态动作解析框架（基于Transformers,Nips 2017,[PDF](https://proceedings.neurips.cc/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf))，采用两个堆叠的转换器作为核心，以动作实例帧作为查询，以存储体中的参数作为键和值。新的框架在时间动作分析上优于基线，它的结构也使它能够以无监督的方式发现一个动作类内和不同动作类之间的子动作段的语义相似性。通过对透明器的研究，我们还可以揭示额外的动作内信息（例如，哪个子动作对某个动作类别的区分度最高）和动作间信息（例如，哪个子动作通常出现在不同的动作类别中）

-  Action Quality Assessment with Temporal Parsing Transformer(**ECCV 2022**) [[PDF](https://arxiv.org/pdf/2207.09270)]
    - 现有的最先进的方法通常依赖于整体视频表示来进行分数回归或排序，这限制了捕捉细粒度类内变化的泛化.
    - 提出了一种时态解析转换器，将整体特征分解为时态部分级表示.具体地说，我们利用一组可学习的查询来表示特定动作的原子时态模式.
    - 现有的AQA数据集不提供时态部分级标签或分区
    - 关键思想是用一组针对特定动作类别的可学习查询来建模共享的原子时态模式
    - 类似于Transformer在自然语言建模中的解码过程，提出了一个时态解析Transformer将每个视频解码为固定数量的部分表示。 为了获得质量分数，我们采用了最近最先进的对比回归框架。 我们的解码机制允许测试视频和样本视频之间的部分表示通过共享的可学习查询隐式对齐。 然后，我们生成每个部分的相对成对表示，并将不同的部分融合在一起进行最终的相对得分回归
    - 提出了两个新的交叉注意响应损失函数：一个是保证可学习查询满足时间顺序的排序损失函数，另一个是提高部分表示的区分度的稀疏损失函数![aqawithtpt](https://user-images.githubusercontent.com/71006202/201813925-4b8952d7-2a65-4960-8eb1-91be21bff29c.png)


### Action Learning
- Set-Supervised Action Learning in Procedural Task Videos via Pairwise Order Consistency(**CVPR 2022**) [[PDF](https://openaccess.thecvf.com/content/CVPR2022/papers/Lu_Set-Supervised_Action_Learning_in_Procedural_Task_Videos_via_Pairwise_Order_CVPR_2022_paper.pdf)] [[Github](https://github.com/ZijiaLewisLu/)]
    - 研究了集合监督的动作学习问题，其目标是利用训练视频中的集合派生形式的弱监督来学习一个动作分割模型
    - 提出了一种基于注意力的方法，该方法引入了一种新的成对排序一致性(POC)损失，鼓励对于同一任务的两个视频中的每个共同动作对，动作的注意力遵循相似的顺序
    - 现有的序列比对方法不同，这些方法将视频中的动作与不同的顺序错位，或者不能可靠地将更多的顺序与更不一致的顺序分开，我们的PoC损失有效地将视频与不同的动作顺序进行比对，并且是可微的，这使得端到端的训练成为可能 ![poc](./POC.png)

### Action Localization
- FineAction: A Fine-Grained Video Dataset for Temporal Action Localization(**ICCV 2021**) [[PDF](https://arxiv.org/pdf/2105.11107)] [[Dataset](https://deeperaction.github.io/datasets/ﬁneaction)]
    - Temporal action localization (TAL) 抽象时态动作定位是视频理解中一个重要而富有挑战性的问题.大多数现有的TAL基准建立在操作类的粗粒度上，这在这项任务中表现出两个主要的限制
    - (1)粗操作会使定位模型在高级上下文信息中过度匹配，而忽略视频中的原子操作细节
    - (2)粗糙的动作类往往会导致时间边界的模糊注释，不利于时间动作的定位
    - 开发了一个新的大规模细粒度视频数据集，称为FineAction，用于时间动作定位.总共包含106个动作类别的103k个时间实例，注释在17k个未修剪的视频中.具有精细动作类的丰富多样性、密集的多实例注释、不同类别的动作同时发生等特点
    - 提出了一个简单的基线方法来处理细粒度的动作检测，在我们的FineAction上实现了13.17%的mAP ![fineaction](./fineaction.png)
- Progressive Attention on Multi-Level Dense Difference Maps for Generic Event Boundary Detection(**CVPR 2022**) [[PDF](https://openaccess.thecvf.com/content/CVPR2022/papers/Tang_Progressive_Attention_on_Multi-Level_Dense_Difference_Maps_for_Generic_Event_CVPR_2022_paper.pdf)] [[Github](https://github.com/MCG-NJU/DDM)]
    - 一般事件边界检测(GEBD)是视频理解中的一个重要任务，旨在检测人类自然感知事件边界的时刻，主要挑战是感知不同事件边界的各种时间变化。
    - 提出了一个有效的、端到端可学习的框架（DDM-NET）解决事件边界的多样性和复杂语义，做了三个显著的改进：
    - （1）构造了一个特征库来存储空间和时间的多层次特征，为多尺度下的差分计算做准备
    - （2）为了缓解以往方法在时间建模方面的不足，我们提出了密集差分映射(DDM)来全面描述运动模式
    - （3）在多级DDM上利用渐进注意来联合聚合外观和运动线索
    - ![image](https://user-images.githubusercontent.com/71006202/201855638-9e509b3c-6877-48ce-aaeb-fb8bb400c81b.png)
    - DDM-NET分别在Kinetics-GEBD和Tapos基准上实现了14%和8%的显著提升

### Video Understanding
- TADA! TEMPORALLY-ADAPTIVE CONVOLUTIONS FOR VIDEO UNDERSTANDING (**ICLR 2021**) [[arxiv](https://arxiv.org/pdf/2110.06178)]
    - 提出了用于视频理解的时间自适应卷积(TADACONV)，表明沿时间维的自适应权值校准是一种有效的方法，可以方便地模拟视频中复杂的时间动态
    - 通过根据帧的局部和全局时间背景来校准每帧的卷积权值，从而使空间卷积具有时间建模能力
    - 在卷积核上操作，而不是在特征上操作，特征的维数比空间分辨率小一个数量级
    - 在多个视频动作识别和定位基准上，与现有的方法相比，至少具有同等或更好的性能
    - TADACONV作为一种简单的插件操作，计算开销可以忽略不计，可以有效地改进现有的许多视频模型
    - ![image](https://user-images.githubusercontent.com/71006202/201856303-8821588e-1122-4811-8ba3-0121e6b9f024.png)
- Bridge-Prompt: Towards Ordinal Action Understanding in Instructional Videos (**CVPR 2022**) [[PDF](https://openaccess.thecvf.com/content/CVPR2022/papers/Li_Bridge-Prompt_Towards_Ordinal_Action_Understanding_in_Instructional_Videos_CVPR_2022_paper.pdf)][[Github](https://github.com/ttlmh/Bridge-Prompt)]
    - 传统的动作识别方法侧重于单个动作的分析。 然而，它们未能充分推理相邻动作之间的上下文关系，而这些上下文关系为理解长视频提供了潜在的时序逻辑
    - 提出了一个基于提示的框架Bridge-Prompt（BR-Prompt）来建模相邻动作之间的语义，从而同时从教学视频(instructional videos)中的一系列顺序动作中挖掘上下文和上下文信息
    - ![image](https://user-images.githubusercontent.com/71006202/201817478-41a338e8-3ddd-4854-b400-60a1d4176731.png)
    - 个体行为标签重新定义为集成的文本提示，以用于监督，弥合了个体行为语义之间的鸿沟。所生成的文本提示与相应的视频剪辑配对，并通过对比方法共同训练文本编码器和视频编码器
    - 学习后的视觉编码器具有更强的下游顺序动作相关任务的能力，如动作分割和人体活动识别
    - 为了分析教学视频，我们不仅需要理解单个动作的语义，还需要学习上下文动作之间的语义关系
    - 然而，基于图的方法是转换的，受到输入节点和/或边的先验知识的限制。 因此，基于图的方法无法解决未知类型的节点，因而***难以扩展和迁移***
    - 现有的行为识别框架下，目前描述人类行为的方法是为每个单个行为分配单独的注释，将不同的行为视为单独的类ID。 这对于识别单独的动作是可行的，但由于单个类ID不能提供上下文信息，因此无法描述顺序动作之间的上下文关系.图1中(a)和(b)的例子进一步说明了传统的基于类ID的方法的局限性
    - 我们发现人类语言是描述相关动作之间顺序语义的有力工具。人类语言能够根据序数和特定句型描述多个顺序发生的事件。例如，拿瓶子和倒水之间的顺序关系可以用“人先拿瓶子，然后倒水”来描述。 语言自然地连接了顺序动作之间的语义
    - 语言可以直观地外推到未知类型的动作。 给定一个把面包放在面包上的新表达式，它的语义可以从已知类型的动作表达式中推断出来。 图1(c)说明了语言表示的有效性
    - 提出了一种基于文本的教学视频分析学习方法:基于自然语言处理(NLP)和视觉识别(Learning transferable visual models from natural language supervision,ICML 21[[PDF]](http://proceedings.mlr.press/v139/radford21a/radford21a.pdf))中基于提示的学习方法的最新进展，我们提出了一个三加一的文本提示设计来分析包含一系列顺序动作的视频片段
    - 开发了一个基于提示的学习框架，在专门设计的视频-文本融合模块的基础上，联合训练视频和文本编码器，从而同时利用上下文和上下文操作信息来更全面地理解教学视频
    - ![image](https://user-images.githubusercontent.com/71006202/201819379-b75284ef-4855-4a72-aed2-c5d3e649387a.png)
    
### Video Reconstruction
- VideoMAE: Masked Autoencoders are Data-Efﬁcient Learners for Self-Supervised Video Pre-Training (**NIPS 2022**) [[PDF](https://paperswithcode.com/paper/videomae-masked-autoencoders-are-data-1)][[Github](https://paperswithcode.com/paper/videomae-masked-autoencoders-are-data-1#code)]
    - 提出了一个简单而有效的视频屏蔽自动编码器，它释放了原始视觉转换器在视频识别方面的潜力。 据我们所知，这是第一个简单使用普通ViT骨干的掩蔽视频预训练框架。 为了解决屏蔽视频建模中的信息泄漏问题，本文提出了一种极高比例的管式屏蔽，提高了视频的性能。
    - ![image](https://user-images.githubusercontent.com/71006202/201860993-5e34eeb8-0369-4211-9e3f-f092e68a92c8.png)
    - 与NLP和图像掩蔽建模的结果相一致，我们的视频证明了这种简单的掩蔽和重建策略为自监督视频预训练提供了一个很好的解决方案。 用我们的Videomae预训练的模型明显优于从零开始训练或用对比学习方法预训练的模型。
    - 我们在掩蔽建模方面获得了额外的重要发现，这些发现在以前的NLP和图像研究中可能被忽略。（1）我们证明了VideoMae是一个数据高效的学习器，只需要3.5K的视频就可以成功地训练它。（2）对于SSVP而言，当源数据集和目标数据集之间存在域转移时，数据质量比数量更重要。
    
# *******E N D*******

# Awesome-Skeleton-based-Action-Recognition <!-- omit in toc -->

If you have any problems, suggestions or improvements, please submit the issue or PR.

## TODO <!-- omit in toc -->

- [ ] Paper list
  - [x] supervised methods
  - [ ] semi-supervised methods
  - [ ] unsupervised methods
  - [ ] adversarial methods
- [ ] Leaderboard for supervised methods
  - [x] NTU RGB+D
  - [ ] NTU RGB+D 120
- [ ] Leaderboard for unsupervised and semi-supervised methods

## Contents <!-- omit in toc -->

- [Misc](#misc)
- [Datasets](#datasets)
- [Semi-supervised and Unsupervised Skeleton Rrepresentation](#semi-supervised-and-unsupervised-skeleton-rrepresentation)
  - [arXiv](#arxiv)
  - [papers](#papers)
- [Supervised Skeleton-based Action Recognition](#supervised-skeleton-based-action-recognition)
  - [arXiv papers](#arxiv-papers)
  - [Survey](#survey)
  - [2020](#2020)
  - [2019](#2019)
  - [2018](#2018)
  - [2017](#2017)
  - [before 2017](#before-2017)
- [LeaderBoard](#leaderboard)
  - [NTU-RGB+D](#ntu-rgbd)
  - [NTU-RGB+D 120](#ntu-rgbd-120)

## Misc

- Microsoft Kinect sensor and its effect (**IEEE Multimedia 2012**) [[paper](https://ieeexplore.ieee.org/document/6190806)]
- Other GITHUB Repos for Skeleton-based Action Recognition Papers
  - [<https://github.com/XiaoCode-er/Skeleton-Based-Action-Recognition-Papers>](https://github.com/XiaoCode-er/Skeleton-Based-Action-Recognition-Papers)
  - [<https://github.com/cagbal/Skeleton-Based-Action-Recognition-Papers-and-Notes>](https://github.com/cagbal/Skeleton-Based-Action-Recognition-Papers-and-Notes)
- [Quo Vadis, Skeleton Action Recognition?](https://skeleton.iiit.ac.in/) : A web portal as part on human action understanding from skeleton data. The
portal contains
  - (1) an interactive dashboard showing detailed performance plots of top performing models for NTU-120 dataset.
  - (2) code and pre-trained models for top-performers, including novel ensemble which achieves state-of-the-art performance on NTU-120
  - (3) new skeleton action datasets (skeletics-152, skeleton-mimetics) and pre-trained models.

## Datasets

- *(New! 2021)* **PoseC3D 2D Skeleton Dataset (FineGYM, NTURGB-D, Kinetics, Volleyball)** [[arxiv](https://arxiv.org/pdf/2104.13586.pdf), [Github](https://github.com/kennymckormick/pyskl)]
- *(New! 2021)* **NTU60-X Dataset** [[arxiv](https://arxiv.org/pdf/2101.11529.pdf), [Github](https://github.com/skelemoa/ntu-x)]

- *(New! 2019)* **NTU RGB+D 120 Dataset** [[Homepage](http://rose1.ntu.edu.sg/datasets/actionrecognition.asp),[Github](https://github.com/shahroudy/NTURGB-D)]
- NTU RGB+D Dataset [[Homepage](http://rose1.ntu.edu.sg/datasets/actionrecognition.asp),[Github](https://github.com/shahroudy/NTURGB-D)]
- (2018) VARYING-VIEW RGB-D ACTION DATASET [[arxiv](https://arxiv.org/pdf/1904.10681.pdf), [Github](https://github.com/HRI-UESTC/CFM-HRI-RGB-D-action-database)]
- (2017) SYSU 3D Human-Object Interaction Dataset (**SYSU**)
- (2015) UWA3D Multiview Activity II Dataset (**UWA3D**) [[download](http://staffhome.ecm.uwa.edu.au/~00053650/databases.html)]
- (2014) Northwestern-UCLA Dataset (**N-UCLA**) [[donwload](https://users.eecs.northwestern.edu/~jwa368/my_data.html)]
<!-- - SBU Kinect Interaction Dataset (**SBU**) -->

This section only shows some popular or new datasets, other available datasets for 3D action recognition and their statistics can be found in the following Table from the journal paper of **NTU RGB+D 120 Dataset** ([TPAMI](https://arxiv.org/pdf/1905.04757.pdf)).
![datasets](./datasets.jpg)

## Semi-supervised and Unsupervised Skeleton Rrepresentation

### arXiv

- **[Kinetic-GAN]** Generative Adversarial Graph Convolutional Networks for Human Action Synthesis (**WACV 2022**)[[arxiv](https://arxiv.org/abs/2110.11191)] [[Github](https://github.com/DegardinBruno/Kinetic-GAN)]
- Augmented skeleton based contrastive action learning with momentum lstm for unsupervised action recognition [[arxiv](https://arxiv.org/abs/2008.00188)] [[Github](https://github.com/LZU-SIAT/AS-CAL)]
- Skeleton-DML: Deep Metric Learning for Skeleton-Based One-Shot Action Recognition [[arxiv](https://arxiv.org/abs/2012.13823)][[Github](https://github.com/raphaelmemmesheimer/skeleton-dml)]
- Sparse Semi-Supervised Action Recognition with Active Learning [[arxiv](https://arxiv.org/abs/2012.01740#:~:text=Sparse%20Semi%2DSupervised%20Action%20Recognition%20with%20Active%20Learning,-Jingyuan%20Li%2C%20Eli&text=Current%20state%2Dof%2Dthe%2D,in%20annotation%20and%20mislabeled%20data.)]
- 3D Human Action Representation Learning via Cross-View Consistency Pursuit (**CVPR 2021**)[[arxiv](https://arxiv.org/pdf/2104.14466.pdf)][[Github](https://github.com/LinguoLi/CrosSCLR)] 
- STAR: Sparse Transformer-based Action Recognition [[arxiv](https://arxiv.org/abs/2107.07089)] [[Github](https://github.com/imj2185/STAR)]

### papers

-  Skeleton-Contrastive 3D Action Representation Learning (**ACM MM 2021**) [[arxiv](https://arxiv.org/pdf/2007.05934.pdf)] [[Github](https://github.com/fmthoker/skeleton-contrast)]
- Adversarial Self-Supervised Learning for Semi-Supervised 3D Action Recognition (**ECCV 2020**) [[arxiv](https://arxiv.org/pdf/2007.05934.pdf)]
- Unsupervised 3D Human Pose Representation with Viewpoint and Pose Disentanglement (**ECCV 2020**) [[arxiv](https://arxiv.org/pdf/2007.07053.pdf)] [[Github](https://github.com/NIEQiang001/unsupervised-human-pose)]
- Predict & cluster: Unsupervised skeleton based action recognition (**CVPR 2020**) [[arxiv](https://arxiv.org/pdf/1911.12409.pdf)] [[Github](https://github.com/shlizee/Predict-Cluster)]
- Ms2l: Multi-task self-supervised learning for skeleton based action recognition (**ACMMM 2020**) [[arxiv](https://arxiv.org/pdf/2010.05599.pdf)]
- Unsupervised feature learning of human actions as trajectories in pose embedding manifold (**WACV 2018**) [[arxiv](https://arxiv.org/abs/1812.02592)]
- Unsupervised representation learning with long-term dynamics for skeleton based action recognition (**AAAI 2018**) [[arxiv](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/viewFile/16341/15984)] [[Github](https://github.com/jungel2star/Unsupervised-Representation-Learning-with-Long-Term-Dynamics-for-Skeleton-Based-Action-Recognition)]

## Skeleton-based Action Recognition under Adversarial Attack

- Understanding the Robustness of Skeleton-based Action Recognition under Adversarial Attack (**CVPR 2021**) [[arxiv](https://arxiv.org/pdf/2103.05347.pdf)]
- BASAR:Black-box Attack on Skeletal Action Recognition (**CVPR 2021**) [[arxiv](https://arxiv.org/pdf/2103.05266.pdf)]

## Supervised Skeleton-based Action Recognition

### arXiv papers

This section only includes the last five papers since 2018 in [arXiv.org](arXiv.org). Note that arXiv papers **without available codes** are not included in [the leaderboard of performance](#leaderboard).

- **[Sym-GNN]** Symbiotic Graph Neural Networks for 3D Skeleton-based Human Action Recognition and Motion Prediction [[arxiv](https://arxiv.org/pdf/1910.02212v1.pdf)] [[Github](https://github.com/limaosen0/Sym-GNN)]
- **[DenseIndRNN]** Deep Independently Recurrent Neural Network (**Preprint**) [[arxiv](https://arxiv.org/pdf/1910.06251v1.pdf)] [[Github](https://github.com/Sunnydreamrain/IndRNN_pytorch)]
- Optimized Skeleton-based Action Recognition via Sparsified Graph Regression [[arxiv](https://arxiv.org/pdf/1811.12013.pdf)]
- Skeleton-Based Action Recognition with Synchronous Local and Non-local Spatio-temporal Learning and Frequency Attention [[arxiv](https://arxiv.org/pdf/1811.04237.pdf)]
- **[DSTA-Net]** Decoupled Spatial-Temporal Attention Network for Skeleton-Based Action Recognition [[arxiv](https://arxiv.org/abs/2007.03263#:~:text=Decoupled%20Spatial%2DTemporal%20Attention%20Network%20for%20Skeleton%2DBased%20Action%20Recognition,-Lei%20Shi%2C%20Yifan&text=It%20involves%20solely%20the%20attention,their%20positions%20or%20mutual%20connections.)]
- Skeleton-Based Action Recognition with Multi-Stream Adaptive Graph Convolutional Networks [[arxiv](https://arxiv.org/pdf/1912.06971.pdf)]
- Quo Vadis, Skeleton Action Recognition ? [[arxiv](https://128.84.21.199/pdf/2007.02072.pdf)] [[Github](https://github.com/skelemoa/quovadis)]
- SynSE: Syntactically Guided Generative Embeddings for Zero Shot Skeleton Action Recognition [[arxiv](https://arxiv.org/pdf/2101.11530.pdf)] [[Github](https://github.com/skelemoa/synse-zsl)]
- Leveraging Third-Order Features in Skeleton-Based Action Recognition [[arxiv](https://arxiv.org/pdf/2105.01563.pdf)][[Github](https://github.com/ZhenyueQin/Angular-Skeleton-Encoding)] 

### Survey

- A Comparative Review of Recent Kinect-based Action Recognition Algorithms (***TIP 2019***) [[arxiv](https://arxiv.org/pdf/1906.09955.pdf)]

### 2022

- **[PoseC3D]** Revisiting Skeleton-based Action Recognition [[paper](https://arxiv.org/pdf/2104.13586.pdf)] [[Code](https://github.com/kennymckormick/pyskl)] (CVPR 2022 Oral)
- **[PSUMNet]** Unified Modality Part Streams are All You Need for Efficient Pose-based Action Recognition (ECCV 2022 WCPA) [[paper](https://arxiv.org/pdf/2208.05775.pdf)][[Github](https://github.com/skelemoa/psumnet)]


### 2021

- **[MMDGCN]** Multi-scale Mixed Dense Graph Convolution Network for Skeleton-based Action Recognition (**IEEE Access**) [[paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9312608)]
- Quo Vadis, Skeleton Action Recognition ? [[paper](https://arxiv.org/pdf/2007.02072.pdf)] [[Github](https://github.com/skelemoa/quovadis)] (**IJCV**)
- Constructing Stronger and Faster Baselines for Skeleton-based Action Recognition [[paper](https://arxiv.org/pdf/2106.15125.pdf)] [[Github](https://github.com/yfsong0709/EfficientGCNv1)] (submitted to **TPAMI**)
- **[CTR-GCN]** Channel-wise Topology Refinement Graph Convolution for Skeleton-Based Action Recognition [[paper](https://arxiv.org/pdf/2107.12213.pdf)] [[Github](https://github.com/Uason-Chen/CTR-GCN)] (**ICCV 2021**)

### 2020

- **[MV-IGNET]** Learning Multi-View Interactional Skeleton Graph for Action Recognition (**TPAMI 2020**) [[paper](https://ieeexplore.ieee.org/abstract/document/9234715)][[Github](https://github.com/niais/mv-ignet)]
- **[P&C FW-AEC]** PREDICT & CLUSTER: Unsupervised Skeleton Based Action Recognition (**CVPR 2020**) [[paper](http://openaccess.thecvf.com/content_CVPR_2020/papers/Su_PREDICT__CLUSTER_Unsupervised_Skeleton_Based_Action_Recognition_CVPR_2020_paper.pdf)]
- **[CA-GC]** Context Aware Graph Convolution for Skeleton-Based Action Recognition (**CVPR 2020**) [[paper](http://openaccess.thecvf.com/content_CVPR_2020/papers/Zhang_Context_Aware_Graph_Convolution_for_Skeleton-Based_Action_Recognition_CVPR_2020_paper.pdf)]
- **[Shift-GCN]** Skeleton-Based Action Recognition With Shift Graph Convolutional Network (**CVPR 2020**) [[paper](http://openaccess.thecvf.com/content_CVPR_2020/papers/Cheng_Skeleton-Based_Action_Recognition_With_Shift_Graph_Convolutional_Network_CVPR_2020_paper.pdf)][[Github](https://github.com/kchengiva/Shift-GCN)]
- **[DMGNN]** Dynamic Multiscale Graph Neural Networks for 3D Skeleton Based Human Motion Prediction (**CVPR 2020**) [[paper](http://openaccess.thecvf.com/content_CVPR_2020/papers/Li_Dynamic_Multiscale_Graph_Neural_Networks_for_3D_Skeleton_Based_Human_CVPR_2020_paper.pdf)]
- **[SGN]** Semantics-Guided Neural Networks for Efficient Skeleton-Based Human Action Recognition (**CVPR 2020**) [[arxiv](https://arxiv.org/pdf/1904.01189.pdf)][[Github](https://github.com/microsoft/SGN)]
- **[MS-G3D]** Disentangling and Unifying Graph Convolutions for Skeleton-Based Action Recognition (**CVPR 2020**) [[arxiv](https://arxiv.org/pdf/2003.14111.pdf)] [[Github](https://github.com/kenziyuliu/ms-g3d)]
- **[Dynamic GCN]** Dynamic GCN: Context-enriched Topology Learning for Skeleton-based Action Recognition (**ACM-MM 2020**)[[arxiv](https://arxiv.org/pdf/2007.14690.pdf)]

- **[GCN-NAS]** Learning Graph Convolutional Network for Skeleton-based Human Action Recognition by Neural Searching (**AAAI 2020**) [[arxiv](https://arxiv.org/pdf/1911.04131v1.pdf)] [[Github](https://github.com/xiaoiker/GCN-NAS)]

- **[DecoupleGCN-DropGraph]** Decoupling GCN with DropGraph Module for Skeleton-Based Action Recognition (**ECCV 2020**) [[arxiv](http://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123690528.pdf)] [[Github](https://github.com/kchengiva/DecoupleGCN-DropGraph)]
- **[PA-ResGCN]** Stronger, Faster and More Explainable: A Graph Convolutional Baseline for Skeleton-based Action Recognition (**ACM-MM 2020**) [[arxiv](https://arxiv.org/pdf/2010.09978.pdf)] [[Github](https://github.com/yfsong0709/ResGCNv1)]
- **[Poincare-GCN]** Mix Dimension in Poincaré Geometry for 3D Skeleton-based Action Recognition (**ACM-MM 2020**) [[arxiv](https://arxiv.org/pdf/2007.15678.pdf)]
- **[STIGCN]** Spatio-Temporal Inception Graph Convolutional for Skeleton-Based Action Recognition (**ACM-MM 2020**) [[arxiv](https://dl.acm.org/doi/pdf/10.1145/3394171.3413666)]
- **[JOLO-GCN]** JOLO-GCN: Mining Joint-Centered Light-Weight Information for Skeleton-Based Action Recognition (**WACV 2021**) [[arxiv](https://arxiv.org/abs/2011.07787)]
- **[ST-TR-AGCN]** Spatial Temporal Transformer Network for Skeleton-based Action Recognition (**Under submission at Computer Vision and Image Understanding (CVIU)**) [[arxiv](https://arxiv.org/pdf/2008.07404.pdf)] [[Github](https://github.com/Chiaraplizz/ST-TR)]
- **[PCRP]** Prototypical Contrast and Reverse Prediction: Unsupervised Skeleton Based Action Recognition [[arxiv](https://arxiv.org/pdf/2011.07236.pdf)] [[Github](https://github.com/Mikexu007/PCRP)]

### 2019

- NTU-RGB+D 120: A Large-Scale Benchmark for 3D Human Activity Understanding (***TPAMI 2019***) [[arxiv](https://arxiv.org/pdf/1905.04757.pdf)] [[Homepage](http://rose1.ntu.edu.sg/datasets/actionrecognition.asp)] [[Github](https://github.com/shahroudy/NTURGB-D)]
- **[VA-NN]** View Adaptive Neural Networks for High Performance Skeleton-based Human Action Recognition (**TPAMI 2019**) [[arxiv](https://arxiv.org/pdf/1804.07453.pdf)] [[Github](https://github.com/microsoft/View-Adaptive-Neural-Networks-for-Skeleton-based-Human-Action-Recognition)]
- Bayesian Graph Convolutional LSTM for Skeleton Based Action Recognition (**ICCV 2019**) [[arxiv](http://openaccess.thecvf.com/content_ICCV_2019/papers/Zhao_Bayesian_Graph_Convolution_LSTM_for_Skeleton_Based_Action_Recognition_ICCV_2019_paper.pdf)]
- **[2s-SDGCN]** Spatial Residual Layer and Dense Connection Block Enhanced Spatial Temporal Graph Convolutional Network for Skeleton-Based Action Recognition (*ICCV Workshop 2019*) [[paper](http://openaccess.thecvf.com/content_ICCVW_2019/papers/SGRL/Wu_Spatial_Residual_Layer_and_Dense_Connection_Block_Enhanced_Spatial_Temporal_ICCVW_2019_paper.pdf)]
- **[DGNN]** Skeleton-Based Action Recognition With Directed Graph Neural Networks (**CVPR 2019**) [[paper](http://openaccess.thecvf.com/content_CVPR_2019/papers/Shi_Skeleton-Based_Action_Recognition_With_Directed_Graph_Neural_Networks_CVPR_2019_paper.pdf)] [[unofficial PyTorch implementation](https://github.com/kenziyuliu/DGNN-PyTorch)]
- **[2s-AGCN]** Two-Stream Adaptive Graph Convolutional Networks for Skeleton-Based Action Recognition (**CVPR 2019**) [[paper](http://openaccess.thecvf.com/content_CVPR_2019/papers/Shi_Two-Stream_Adaptive_Graph_Convolutional_Networks_for_Skeleton-Based_Action_Recognition_CVPR_2019_paper.pdf)] [[Github](https://github.com/lshiwjx/2s-AGCN)]
- **[AS-GCN]** Actional-Structural Graph Convolutional Networks for Skeleton-based Action Recognition (**CVPR 2019**) [[arxiv](https://arxiv.org/pdf/1904.12659.pdf)] [[Github](https://github.com/limaosen0/AS-GCN)]
- **[AGC-LSTM]** An Attention Enhanced Graph Convolutional LSTM Network for Skeleton-Based Action Recognition (**CVPR 2019**) [[arxiv](https://arxiv.org/pdf/1902.09130.pdf)]
- **[Motif-STGCN]** Graph CNNs with Motif and Variable Temporal Block for Skeleton-based Action Recognition (**AAAI 2019**) [[arxiv](http://geometrylearning.com/paper/Graph_CNN.pdf)] [[Github](https://github.com/wenyh1616/motif-stgcn)]
- Richly Activated Graph Convolutional Network for Action Recognition with Incomplete Skeletons (**ICIP 2019**) [[arxiv](https://arxiv.org/pdf/1905.06774.pdf)] [[Github](https://github.com/yfsong0709/RA-GCNv1)]
- **[TSRJI]** Skeleton Image Representation for 3D Action Recognition based on Tree Structure and Reference Joints (**SIBGRAPI**) [[arxiv](https://arxiv.org/pdf/1909.05704v1.pdf)] [[Github](https://github.com/carloscaetano/skeleton-images#skeleton-images-representation-SkeleMotion-and-SRJI)]
- **[SkeleMotion]** SkeleMotion: A New Representation of Skeleton Joint Sequences Based on Motion Information for 3D Action Recognition (**AVSS**) [[arxiv](https://arxiv.org/pdf/1907.13025v1.pdf)] [[Github](https://github.com/carloscaetano/skeleton-images#skeleton-images-representation-SkeleMotion-and-SRJI)]

### 2018

- **Beyond Joints:** Learning Representations from Primitive Geometries for Skeleton-based Action Recognition and Detection (***TIP 2018***) [[paper](https://ieeexplore.ieee.org/document/8360391)] [[Github](https://github.com/hongsong-wang/Beyond-Joints)]
- **[DPRL]** Deep progressive reinforcement learning for skeleton-based action recognition (**CVPR 2018**) [[paper](http://openaccess.thecvf.com/content_cvpr_2018/papers/Tang_Deep_Progressive_Reinforcement_CVPR_2018_paper.pdf)]
- **[SR-TSL]** Skeleton based action recognition with spatial reasoning and temporal stack learning (**ECCV 2018**) [[arxiv](https://arxiv.org/pdf/1805.02335.pdf)]
- **[HCN]** Co-occurrence feature learning from skeleton data for action recognition and detection with hierarchical aggregation (**IJCAI 2018**) [[arxiv](https://arxiv.org/pdf/1804.06055.pdf)] [[Reimplementation](https://github.com/huguyuehuhu/HCN-pytorch)]
- **[MAN]** Memory attention networks for skeleton-based action recognition (**IJCAI 2018**) [[arxiv](https://arxiv.org/pdf/1804.08254.pdf)] [[Github](https://github.com/memory-attention-networks/MANs)]
- **[ST-GCN]** Spatial temporal graph convolutional networks for skeleton-based action recognition (**AAAI 2018**) [[arxiv](https://arxiv.org/pdf/1801.07455.pdf)] [[Github](https://github.com/yysijie/st-gcn)]
- Spatio-temporal graph convolution for skeleton based action recognition (**AAAI 2018**) [[arxiv](https://arxiv.org/pdf/1802.09834.pdf)]
- Part-based Graph Convolutional Network for Action Recognition (**BMVC 2018**) [[arxiv](https://arxiv.org/pdf/1809.04983.pdf)] [[Github](https://github.com/kalpitthakkar/pb-gcn)]
- A Fine-to-Coarse Convolutional Neural Network for 3D Human Action Recognition (**BMVC 2018**) [[arxiv](https://arxiv.org/pdf/1805.11790.pdf)]
- A Large-scale Varying-view RGB-D Action Dataset for Arbitrary-view Human Action Recognition (**ACMMM 2018**) [[arxiv](https://arxiv.org/pdf/1904.10681.pdf)]

### 2017

- Jointly learning heterogeneous features for RGB-D activity recognition (***TPAMI 2017***) [[paper](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Hu_Jointly_Learning_Heterogeneous_2015_CVPR_paper.pdf)]
- **[Visualization CNN]** Enhanced skeleton visualization for view invariant human action recognition (***Pattern Recognition 2017***) [[paper](https://www.utdallas.edu/~cxc123730/PR_2017.pdf)]
- Global context-aware attention lstm networks for 3d action recognition (**CVPR 2017**) [[paper](https://ieeexplore.ieee.org/document/8099874)]
- **[Two-stream RNN]** Modeling temporal dynamics and spatial configurations of actions using two-stream recurrent neural networks (**CVPR 2017**) [[arxiv](https://arxiv.org/pdf/1704.02581.pdf)] [[Github](https://github.com/hongsong-wang/RNN-for-skeletons)]
- **[C-CNN + MTLN]** A new representation of skeleton sequences for 3d action recognition (**CVPR 2017**) [[arxiv](https://arxiv.org/pdf/1703.03492.pdf)]
- **[Ensemble TS-LSTM]** Ensemble deep learning for skeleton-based action recognition using temporal sliding lstm networks (**ICCV 2017**) [[paper](http://openaccess.thecvf.com/content_ICCV_2017/papers/Lee_Ensemble_Deep_Learning_ICCV_2017_paper.pdf)] [[Github](https://github.com/InwoongLee/TS-LSTM)]
- **[VA-LSTM]** View adaptive recurrent neural networks for high performance human action recognition from skeleton data (**ICCV 2017**) [[arxiv](https://arxiv.org/pdf/1703.08274.pdf)]
- Learning action recognition model from depth and skeleton videos (**ICCV 2017**) [[paper](https://ieeexplore.ieee.org/document/8237883)]
- **[STA-LSTM]** An end-to-end spatio-temporal attention model for human action recognition from skeleton data (**AAAI 2017**) [[arxiv](https://arxiv.org/pdf/1611.06067.pdf)]
- Skeleton-based action recognition using LSTM and CNN (*ICME Workshop 2017*) [[arxiv](https://arxiv.org/pdf/1707.02356.pdf)]
- Skeleton-based action recognition with convolutional neural networks (*ICME Workshop 2017*) [[arxiv](https://arxiv.org/pdf/1704.07595.pdf)]
- PKU-MMD: A large scale benchmark for continuous multi-modal human action understanding (*ACMMM Workshop 2017*) [[arxiv](https://arxiv.org/pdf/1703.07475.pdf)]
- **[Temporal Conv]** Interpretable 3d human action analysis with temporal convolutional networks (*CVPR Workshop 2017*) [[arxiv](https://arxiv.org/pdf/1704.04516.pdf)]

### before 2017

- **[Trust Gate ST-LSTM]** Spatio-temporal lstm with trust gates for 3d human action recognition (**ECCV 2016**) [[arxiv](https://arxiv.org/pdf/1607.07043.pdf)] [[Github](https://github.com/kinect59/Spatio-Temporal-LSTM)]
- **[Part-aware LSTM]** NTU RGB+D: A Large Scale Dataset for 3D Human Activity Analysis (**CVPR 2016**) [[arxiv](https://arxiv.org/pdf/1604.02808.pdf)]
- Rolling rotations for recognizing human actions from 3d skeletal data (**CVPR 2016**) [[paper](https://ieeexplore.ieee.org/document/7780853)]
- Co-occurrence feature learning for skeleton based action recognition using regularized deep lstm networks (**AAAI 2016**) [[paper](https://www.aaai.org/ocs/index.php/AAAI/AAAI16/paper/download/11989/12149)]
- Skeleton based action recognition with convolutional neural network (**ACPR 2015**) [[paper](https://ieeexplore.ieee.org/abstract/document/7486569)]
- **[H-RNN]** Hierarchical recurrent neural network for skeleton based action recognition (**CVPR 2015**) [[paper](https://ieeexplore.ieee.org/document/7298714)]
- Jointly learning heterogeneous features for rgb-d activity recognition (**CVPR 2015**) [[paper](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Hu_Jointly_Learning_Heterogeneous_2015_CVPR_paper.pdf)]
- **[LieGroup]** Human action recognition by representing 3d skeletons as points in a lie group (**CVPR 2014**) [[paper](https://openaccess.thecvf.com/content_cvpr_2014/papers/Vemulapalli_Human_Action_Recognition_2014_CVPR_paper.pdf)]
- Human action recognition using a temporal hierarchy of covariance descriptors on 3d joint locations (**IJCAI 2013**) [[paper](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.415.8032&rep=rep1&type=pdf)]

## LeaderBoard

The section is being continually updated. We only show results on large-scale dataset NTU-RGB+D and NTU-RGB+D 120.

### NTU-RGB+D

| Year | Methods               | Cross-Subject | Cross-View |
| ---- | --------------------- | :-----------: | :--------: |
| 2014 | Lie Group             |     50.1      |    52.8    |
| 2015 | H-RNN                 |     59.1      |    64.0    |
| 2016 | Part-aware LSTM       |     62.9      |    70.3    |
| 2016 | Trust Gate ST-LSTM    |     69.2      |    77.7    |
| 2017 | Two-stream RNN        |     71.3      |    79.5    |
| 2017 | STA-LSTM              |     73.4      |    81.2    |
| 2017 | Ensemble TS-LSTM      |     74.6      |    81.3    |
| 2017 | Visualization CNN     |     76.0      |    82.6    |
| 2017 | C-CNN + MTLN          |     79.6      |    84.8    |
| 2017 | Temporal Conv         |     74.3      |    83.1    |
| 2017 | VA-LSTM               |     79.4      |    87.6    |
| 2018 | Beyond Joints         |     79.5      |    87.6    |
| 2018 | ST-GCN                |     81.5      |    88.3    |
| 2018 | DPRL                  |     83.5      |    89.8    |
| 2019 | Motif-STGCN           |     84.2      |    90.2    |
| 2018 | HCN                   |     86.5      |    91.1    |
| 2018 | SR-TSL                |     84.8      |    92.4    |
| 2018 | MAN                   |     82.7      |    93.2    |
| 2019 | RA-GCN                |     85.9      |    93.5    |
| 2019 | DenseIndRNN           |     86.7      |    93.7    |
| 2018 | PB-GCN                |     87.5      |    93.2    |
| 2019 | AS-GCN                |     86.8      |    94.2    |
| 2019 | VA-NN (fusion)        |     89.4      |    95.0    |
| 2019 | AGC-LSTM (Joint&Part) |     89.2      |    95.0    |
| 2019 | 2s-AGCN               |     88.5      |    95.1    |
| 2020 | SGN                   |     89.0      |    94.5    |
| 2020 | GCN-NAS               |     89.4      |    95.7    |
| 2019 | 2s-SDGCN              |     89.6      |    95.7    |
| 2019 | DGNN                  |     89.9      |    96.1    |
| 2020 | MV-IGNET              |     89.2      |    96.3    |
| 2020 | 4s Shift-GCN          |     90.7      |    96.5    |
| 2020 | DecoupleGCN-DropGraph |     90.8      |    96.6    |  
| 2020 | PA-ResGCN-B19         |     90.9      |    96.0    |
| 2020 | MS-G3D                |     91.5      |    96.2    |
| 2021 | EfficientGCN-B4       |     91.7      |    95.7    |
| 2021 | CTR-GCN               |     92.4      |    96.8    |
| 2022 | PoseC3D               |     94.1      |    97.1    |
| 2022 | PSUMNet               |     92.9      |    96.7    |

### NTU-RGB+D 120

Most of existing methods have not been tested on this new dataset yet, and some results can be found in the paper of **NTU RGB+D 120 Dataset** ([TPAMI](https://arxiv.org/pdf/1905.04757.pdf)).

| Year | Methods                             | Cross-Subject | Cross-Setup |
| ---- | ----------------------------------- | :-----------: | :---------: |
| 2019 | SkeleMotion (Magnitude-Orientation) |     62.9      |    63.0     |
| 2019 | SkeleMotion + Yang *et al*          |     67.7      |    66.9     |
| 2019 | TSRJI                               |     67.9      |    59.7     |
| 2020 | SGN                                 |     79.2      |    81.5     |
| 2020 | MV-IGNET                            |     83.9      |    85.6     |
| 2020 | 4s Shift-GCN                        |     85.9      |    87.6     |
| 2020 | DecoupleGCN-DropGraph               |     86.5      |    88.1     |
| 2020 | MS-G3D                              |     86.9      |    88.4     |
| 2022 | PoseC3D                             |     86.9      |    90.3     |
| 2020 | PA-ResGCN-B19                       |     87.3      |    88.3     |
| 2021 | EfficientGCN-B4                     |     88.3      |    89.1     |
| 2021 | CTR-GCN                             |     88.9      |    90.6     |
| 2022 | PSUMNet                             |     89.4      |    90.6     |
