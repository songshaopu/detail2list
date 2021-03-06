# 预览地址 #
[https://luchanan.github.io/detail2list/index.html](https://luchanan.github.io/detail2list/index.html)

# 背景 #
1. h5上拉刷新来实现分页，当有很多页的话，点击列表某一页去详细，然后从详情返回上一页，可能刷新上一页，位置不能保持，体验不好
2. 列表使用a链接过去的，详情使用window.history.go(-1)返回，有些浏览器不刷新上一页（ios中safari,UC等），有些页面刷新上一页（ios中微信等）
3. 有说使用单页的话，可以保持。但是之前用过angular1.X来实现单页，返回貌似也有这个问题（重新执行了列表js），最近在github看到有用vue实现了这个的效果：[https://github.com/lzxb/vue-cnode?from=xitu](https://github.com/lzxb/vue-cnode?from=xitu)
4. 有说列表用window.open，详情用window.history.go(-1)，h5实践了，不可以

#弊端#
1. 这种适合点列表某个item到详细，然后返回的时候，某个item里面的一些元素没有发生交互变化。
2. 如果要实现这种，比如消息列表点击某个未读item，跳到详情，然后返回来，这个item从未读变为已读。这个需要自己想办法处理

# 想到的办法 #
1. 改交互方式，把上拉刷新改为类似美团美食h5那样，手动点下一页，稍微简单些（主要考虑了有上面弊端2的那种情况）
2. 保持这样上拉刷新这样的交互方式。本地保存数据，记录滚动位置（插件采用这种方式）
3. 列表记录当前页码，到顶部请求上一页，到底部请求下一页。（好麻烦，先放弃，位置也不准确了）

# 插件一些说明 #
1. 列表滚动使用锚点获取scrollTop值，标志是否返回了列表
2. localStorage有过期时间，不用sessionStorage主要是因为有些安卓机的浏览器，跳页面会获取不到sessionStorage值，比如UA:Mozilla/5.0 (Linux; U; Android 5.0.2; zh-CN; Redmi Note 2 Build/LRX22G) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/40.0.2214.89 UCBrowser/11.2.0.880 Mobile Safari/537.36
3. 只有返回列表才执行本地数据，index.html到list.html会重新请求数据。
