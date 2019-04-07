# 限流算法（记录cyc大佬的专栏）

<a name="bf652123"></a>
# 限流的必要性
如果一段时间内请求的数量过大，就会给服务器造成很大压力，可能导致服务器无法提供其它服务。<br /><br />
<a name="0247e605"></a>
# 计数器算法

<br />![](https://cdn.nlark.com/yuque/0/2019/png/245346/1554645907283-56238e88-ae45-44f4-a7f6-b40be6f93e30.png#align=left&display=inline&height=235&originHeight=235&originWidth=451&size=0&status=done&width=451)<br /><br />通过一个计数器 counter 来统计一段时间内请求的数量，并且在指定的时间之后重置计数器。<br /><br />该方法实现简单，但是有临界问题。例如，允许一分钟内通过的请求数为 N，如果在重置计数器的前后一小段时间内分别请求 N 次，那么在这一小段时间内总共请求了 2N 次，超出了规定的 N 次。<br /><br />![](https://cdn.nlark.com/yuque/0/2019/png/245346/1554645936044-b45a3aa4-1386-4a46-918b-0b8438ff8039.png#align=left&display=inline&height=241&originHeight=241&originWidth=480&size=0&status=done&width=480)<br />

<a name="526531cf"></a>
# 滑动窗口算法
是计数器算法的一种改进，将原来的一个时间窗口划分成多个时间窗口，并且不断向右滑动该窗口。<br /><br />![](https://cdn.nlark.com/yuque/0/2019/png/245346/1554645987066-4f4cc7b4-bd5d-4608-bf68-8ecd9bcaef7f.png#align=left&display=inline&height=190&originHeight=208&originWidth=817&size=0&status=done&width=746)<br />在临界位置的突发请求都会被算到时间窗口内，因此可以解决计数器算法的临界问题。<br /><br />![](https://cdn.nlark.com/yuque/0/2019/png/245346/1554646001899-4909f091-5043-4042-ae9a-91be3905ff04.png#align=left&display=inline&height=190&originHeight=207&originWidth=811&size=0&status=done&width=746)
<a name="96bebf4c"></a>
# 漏桶算法
能够以恒定速率处理请求。<br /><br /><br /><br />请求需要先放入缓存中，当缓存满了时，请求会被丢弃。<br /><br />![](https://cdn.nlark.com/yuque/0/2019/png/245346/1554646265489-80ef15f0-6af6-4af1-93e3-f7723aa21c47.png#align=left&display=inline&height=445&originHeight=498&originWidth=835&size=0&status=done&width=746)<br />

<a name="ec89b432"></a>
# 令牌桶算法
和漏桶算法的区别在于它是以恒定速率添加令牌，当一个请求到来时，先从令牌桶取出一个令牌，如果能取到令牌那么就可以处理该请求。<br />
<br />令牌桶的大小有限，超过一定的令牌之后再添加进来的令牌会被丢弃。

令牌桶算法允许突发请求，因为令牌桶存放了很多令牌，那么大量的突发请求会被执行。但是它不会出现临界问题，在令牌用完之后，令牌是以一个恒定的速率添加到令牌桶中的，因此不能再次发送大量突发请求。

![](https://cdn.nlark.com/yuque/0/2019/png/245346/1554646360254-4838c50f-8071-45b1-9228-55b486f37cb2.png#align=left&display=inline&height=453&originHeight=550&originWidth=905&size=0&status=done&width=746)

* [Leaky Bucket & Tocken Bucket - Traffic shaping](https://www.slideshare.net/vimal25792/leaky-bucket-tocken-buckettraffic-shaping)

<br />
