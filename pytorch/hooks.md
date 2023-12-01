Hook钩子

hook是在特定事件后自动执行的函数

pytorch为每个张量或nn.Module对象注册hook，hook由对象的前向或后向传播触发。

总之，就一句话。

**给某一个moudle注册一个钩子，我们就可以获得这一个moudle的输入和输出了，之后我们就可以对这个输入和输出进行操作。**

#### register_forward_hook

钩子函数不应修改输入和输出，并且在使用后应及时删除，以避免每次都运行钩子增加运行负载。

hook(module, input, output) -> None

hook不应该修改 input和output的值。 这个函数返回一个 **句柄(handle)**。它有一个方法 handle.remove()，可以用这个方法将hook从module移除。

```
def register_forward_hook(self, hook):

       handle = hooks.RemovableHandle(self._forward_hooks)
       self._forward_hooks[handle.id] = hook
       return handle
```

```
def __call__(self, *input, **kwargs):
   result = self.forward(*input, **kwargs)
   for hook in self._forward_hooks.values():
       #将注册的hook拿出来用
       hook_result = hook(self, input, result)
   ...
   return result
```

当我们执行model(x)的时候，底层主要使用forward()方法计算结果，运行钩子函数。

```
def hook(module, inputdata, output):
    '''把这层的输出拷贝到features中'''
    print(output.data)
 
handle = net.conv2.register_forward_hook(hook)
net(img)
# 用完hook后删除
handle.remove()
```

#### register_backward_hook：

```
def register_backward_hook(self, hook):
    handle = hooks.RemovableHandle(self._backward_hooks)
    self._backward_hooks[handle.id] = hook
    return handle
```

