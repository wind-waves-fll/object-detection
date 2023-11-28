# 目标检测

1. 一个关于目标检测的网站，记录了目标检测发展过程中的大多数论文。[Object Detection - handong1587](https://handong1587.github.io/deep_learning/2015/10/09/object-detection.html)

- Anchor-base

  深度学习目标检测通常都被建模成对一些候选区域进行分类和回归的问题。在单阶段检测器中，这些候选区域就是通过滑窗方式产生的 anchor；在两阶段检测器中，候选区域是 RPN 生成的 proposal，但是 RPN 本身仍然是对滑窗方式产生的 anchor 进行分类和回归。

  - Two-stage Object Detection
  - Single-shot Object Detection

- Anchor-free

  anchor-free是通过另外一种手段来解决检测问题的。同样分为两个子问题，即确定物体中心和对四条边框的预测。预测物体中心时，将中心预测融入到类别预测的 target 里面，也可以预测一个 soft 的 centerness score。对于四条边框的预测，则比较一致，都是预测该像素点到 ground truth 框的四条边距离，不过会使用一些 trick 来限制 regress 的范围。

- Transformers

- Weakly Supervised Object Detection

- Zero-shot Object Detection